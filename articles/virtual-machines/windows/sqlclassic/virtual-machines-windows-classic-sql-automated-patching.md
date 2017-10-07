---
title: "aaaAutomated aplicação de patches para VMs do SQL Server (clássico) | Microsoft Docs"
description: "Explica o recurso de aplicação de patch automatizada hello para SQL Server máquinas virtuais em execução no Azure usando o modo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Clássico)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Clássico](../classic/sql-automated-patching.md)
> 
> 

A aplicação de patch automatizada estabelece uma janela de manutenção para uma Máquina Virtual do Azure que executa o SQL Server. Atualizações automáticas só podem ser instaladas durante esta janela de manutenção. Para o SQL Server, isso garante que as atualizações do sistema e qualquer reinicialização associada ocorre no melhor tempo possível Olá para o banco de dados de saudação. Aplicação de patch automatizada depende Olá [extensão do SQL Server IaaS Agent](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. versão do Gerenciador de recursos de saudação tooview deste artigo, consulte [aplicação de patch automatizada para o SQL Server no Gerenciador de recursos de máquinas virtuais do Azure](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Pré-requisitos
toouse aplicação de patch automatizada, considere Olá pré-requisitos a seguir:

**Sistema operacional**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versão do SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview).

**Extensão IaaS do SQL Server**:

* [Instalar Olá extensão do SQL Server IaaS](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Configurações
Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para aplicação de patch automatizada. Para VMs clássicas, você deve usar PowerShell tooconfigure essas configurações.

| Configuração | Valores possíveis | Descrição |
| --- | --- | --- |
| **Aplicação de patch automatizada** |Habilitar/desabilitar (Desabilitado) |Habilita ou desabilita a Aplicação de Patch Automatizada para uma máquina virtual do Azure. |
| **Agenda de manutenção** |Todos os dias, segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira, sábado e domingo |agenda de saudação para baixar e instalar atualizações do Windows, SQL Server e Microsoft para sua máquina virtual. |
| **Hora de início da manutenção** |0h a 24h |Olá início local tempo tooupdate Olá VM. |
| **Duração da janela de manutenção** |30-180 |número de saudação de minutos permitidos download de saudação toocomplete e instalação de atualizações. |
| **Categoria de patch** |Importante |categoria de saudação do toodownload atualizações e instalar. |

## <a name="configuration-with-powershell"></a>Configuração com o PowerShell
Olá exemplo a seguir, PowerShell é usado tooconfigure aplicação de patch automatizada em uma VM existente do SQL Server. Olá **New-AzureVMSqlServerAutoPatchingConfig** comando configura uma nova janela de manutenção para atualizações automáticas.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

Com base neste exemplo, hello tabela a seguir descreve a efeito prático Olá no destino Olá VM do Azure:

| Parâmetro | Efeito |
| --- | --- |
| **DayOfWeek** |Patches instalados toda quinta-feira. |
| **MaintenanceWindowStartingHour** |Inicia as atualizações às 11h. |
| **MaintenanceWindowsDuration** |Os patches devem ser instalados dentro de 120 minutos. Com base na hora de início do hello, elas devem concluir até 1:00 pm. |
| **PatchCategory** |Olá, somente a configuração possíveis para esse parâmetro é "Importante". |

Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.

toodisable aplicação de patch automatizada, Olá execução mesmo script sem Olá - Enable parâmetro toohello New-AzureVMSqlServerAutoPatchingConfig. Como com a instalação, pode levar várias toodisable de minutos aplicação de patch automatizada.

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](../classic/sql-server-agent-extension.md).

Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

