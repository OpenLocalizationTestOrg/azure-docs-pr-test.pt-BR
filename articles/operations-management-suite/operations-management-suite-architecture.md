---
title: aaaOperations arquitetura Management Suite (OMS) | Microsoft Docs
description: "O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem.  Este artigo identifica Olá serviços diferentes incluídos no OMS e fornece links tootheir detalhadas conteúdo."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>Arquitetura do OMS
O [OMS (Operations Management Suite)](https://azure.microsoft.com/documentation/services/operations-management-suite/) é uma coleção de serviços baseados em nuvem para gerenciar seus ambientes locais e na nuvem.  Este artigo descreve Olá diferentes locais e na nuvem componentes do OMS e sua arquitetura de computação em nuvem de alto nível.  Você pode consultar a documentação de toohello para cada serviço para obter mais detalhes.

## <a name="log-analytics"></a>Log Analytics
Todos os dados coletados pelo [análise de Log](https://azure.microsoft.com/documentation/services/log-analytics/) é armazenado no repositório do OMS Olá que é hospedado no Azure.  Fontes conectadas geram dados coletados no repositório do OMS hello.  Atualmente, há três tipos de fontes conectadas com suporte.

* Um agente instalado em um [Windows](../log-analytics/log-analytics-windows-agents.md) ou [Linux](../log-analytics/log-analytics-linux-agents.md) computador conectado diretamente tooOMS.
* Um grupo de gerenciamento do System Center Operations Manager (SCOM) [conectado tooLog análise](../log-analytics/log-analytics-om-agents.md) .  Agentes SCOM continuam toocommunicate com servidores de gerenciamento que encaminham eventos e dados de desempenho tooLog análise.
* Uma [conta de armazenamento do Azure](../log-analytics/log-analytics-azure-storage.md) que coleta dados do [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) por meio de uma função de trabalho, função web ou máquina virtual no Azure.

Fontes de dados definem dados Olá que coleta de análise de Log de fontes conectadas, incluindo logs de eventos e contadores de desempenho.  Soluções adicionar funcionalidade tooOMS e podem ser facilmente adicionadas tooyour de espaço de trabalho de saudação [Galeria de soluções do OMS](../log-analytics/log-analytics-add-solutions.md).  Algumas soluções podem exigir uma conexão direta de tooLog análise dos agentes SCOM enquanto outros podem exigir um toobe adicionais agente instalado.

Análise de log tem um portal baseado na web que você pode usar recursos do OMS toomanage, adicionar e configurar soluções do OMS e exibir e analisar dados no repositório do OMS hello.

![Arquitetura de alto nível do Log Analytics](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Automação do Azure
[Runbooks de automação do Azure](http://azure.microsoft.com/documentation/services/automation) são executados na nuvem do Azure de saudação e pode acessar recursos no Azure, em outros serviços em nuvem, ou acessíveis pela Internet pública de hello.  Você também pode designar computadores locais em seu data center local usando o [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md) para que os runbooks possam acessar recursos locais.

[Configurações DSC](../automation/automation-dsc-overview.md) armazenadas na automação do Azure podem ser aplicadas diretamente tooAzure VMs.  Outras máquinas físicas e virtuais podem solicitar configurações do servidor de pull de DSC de automação do Azure hello.

Automação do Azure tem uma solução do OMS que exibe estatísticas e links toolaunch Olá portal do Azure para todas as operações.

![Arquitetura de alto nível da Automação do Azure](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Serviço de Backup do Azure
Os dados protegidos no [Backup do Azure](http://azure.microsoft.com/documentation/services/backup) são armazenados em um cofre de backup localizado em uma região geográfica específica.  Olá dados são replicados dentro Olá mesma região e, dependendo do tipo de saudação do cofre, também pode ser o tooanother replicado região para redundância adicional.

O Backup do Azure apresenta três cenários fundamentais.

* Computador com Windows com o agente do Backup do Azure.  Isso permite que você toobackup arquivos e pastas a partir de qualquer servidor ou cliente Windows diretamente tooyour Cofre de backup do Azure.  
* DPM (System Center Data Protection Manager) ou Servidor de Backup do Microsoft Azure. Isso permite que você tooleverage DPM ou servidor de Backup do Microsoft Azure toobackup arquivos e pastas além de cargas de trabalho de tooapplication como armazenamento de toolocal SQL e SharePoint e, em seguida, replicar tooyour Cofre de backup do Azure.
* Extensões da Máquina Virtual do Azure.  Isso permite que máquinas virtuais do Azure de toobackup tooyour Cofre de backup do Azure.

Backup do Azure tem uma solução do OMS que exibe estatísticas e links toolaunch Olá portal do Azure para todas as operações.

![Arquitetura de alto nível do Backup do Azure](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) orquestra a replicação, o failover e o failback de máquinas virtuais e servidores físicos. Dados de replicação são trocados entre hosts Hyper-V, hipervisores VMware e servidores físicos em datacenters primários e secundários, ou entre Olá datacenter e o armazenamento do Azure.  A Recuperação de Site armazena os metadados em cofres localizados em determinada região geográfica do Azure. Nenhum dado replicado é armazenado pelo Olá serviço de recuperação de Site.

O Azure Site Recovery apresenta três cenários fundamentais de replicação.

**Replicação de máquinas virtuais Hyper-V**

* Se as máquinas virtuais Hyper-V são gerenciadas em nuvens do VMM, você pode replicar tooa secundário data center ou tooAzure armazenamento.  TooAzure de replicação é uma conexão segura de internet.  Data Center secundário de tooa de replicação é Olá LAN.
* Se as máquinas virtuais Hyper-V não são gerenciadas pelo VMM, você pode replicar somente o armazenamento tooAzure.  TooAzure de replicação é uma conexão segura de internet.

**Replicação de máquinas virtuais VMWare**

* Você pode replicar VMware máquinas virtuais tooa data center secundário executando o VMware ou tooAzure de armazenamento.  TooAzure de replicação pode ocorrer através de uma VPN de site a site ou rota expressa do Azure ou em uma conexão segura de Internet. Data Center secundário de tooa de replicação ocorre sobre Olá canal de dados do InMage Scout.

**Replicação de servidores físicos do Windows e Linux** 

* Você pode replicar os servidores físicos tooa datacenter ou tooAzure armazenamento secundário. TooAzure de replicação pode ocorrer através de uma VPN de site a site ou rota expressa do Azure ou em uma conexão segura de Internet. Data Center secundário de tooa de replicação ocorre sobre Olá canal de dados do InMage Scout.  O Azure Site Recovery tem uma solução do OMS que exibe algumas estatísticas, mas você deve usar o hello portal do Azure para qualquer operação.

![Arquitetura de alto nível do Azure Site Recovery](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Saiba mais sobre a [Automação do Azure](https://azure.microsoft.com/documentation/services/automation).
* Saiba mais sobre o [Backup do Azure](http://azure.microsoft.com/documentation/services/backup).
* Saiba mais sobre o [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

