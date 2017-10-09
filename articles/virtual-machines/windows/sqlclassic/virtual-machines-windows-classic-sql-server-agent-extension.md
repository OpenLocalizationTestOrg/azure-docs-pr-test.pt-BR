---
title: "tarefas de gerenciamento de aaaAutomate em VMs do SQL (clássico) | Microsoft Docs"
description: "Este tópico descreve como toomanage Olá extensão do agente do SQL Server, que automatiza tarefas de administração do SQL Server específicas. Entre elas estão o Backup Automatizado, a Aplicação de Patch Automatizada e a Integração do Cofre de Chaves do Azure. Este tópico usa o modo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Automatizar tarefas de gerenciamento em máquinas virtuais do Azure com hello extensão do SQL Server Agent (clássico)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Clássico](../classic/sql-server-agent-extension.md)
> 
>
 
Olá extensão do agente IaaS do SQL Server (SQLIaaSAgent) é executado em máquinas virtuais do Azure tooautomate as tarefas de administração. Este tópico fornece uma visão geral dos serviços de saudação suportados pela extensão de hello, bem como instruções de instalação, status e remoção.

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. versão do Gerenciador de recursos de saudação tooview deste artigo, consulte [extensão do SQL Server Agent para o SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Serviços com suporte
Olá extensão do SQL Server IaaS Agent dá suporte a saudação tarefas de administração a seguir:

| Recurso de administração | Descrição |
| --- | --- |
| **Backup Automatizado do SQL** |Automatiza Olá agendamento de backups para todos os bancos de dados para instância padrão de saudação do SQL Server na VM de saudação. Para saber mais, veja [Backup automatizado para o SQL Server em Máquinas Virtuais do Azure (Clássico)](../classic/sql-automated-backup.md). |
| **Aplicação de patch automatizada do SQL** |Configura uma janela de manutenção durante as atualizações tooyour VM pode levar coloca, para que você possa evitar atualizações durante horários de pico para sua carga de trabalho. Para obter mais informações, confira [Aplicação de patch automatizada para SQL Server em máquinas virtuais do Azure (Clássico)](../classic/sql-automated-patching.md). |
| **Integração do Cofre da Chave do Azure** |Permite que você tooautomatically instalar e configurar o Cofre de chaves do Azure na VM do SQL Server. Para saber mais, confira [Configurar a Integração do Cofre de Chaves do Azure para o SQL Server em VMs do Azure (Clássico)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Pré-requisitos
Requisitos toouse Olá extensão do SQL Server IaaS Agent na sua VM:

### <a name="operating-system"></a>Sistema operacional:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>Versões do SQL Server:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>PowerShell do Azure:
[Baixar e configurar os comandos do PowerShell do Azure mais recentes Olá](/powershell/azure/overview).

Inicie o Windows PowerShell e conectá-lo tooyour assinatura do Azure com hello **Add-AzureAccount** comando.

    Add-AzureAccount

Se você tiver várias assinaturas, use **Select-AzureSubscription** tooselect assinatura de saudação que contém o VM clássico.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

Neste ponto, você pode obter uma lista de máquinas virtuais clássicas de saudação e seus nomes de serviço associado com hello **Get-AzureVM** comando.

    Get-AzureVM

## <a name="installation"></a>Instalação
Para VMs clássicas, você deve usar o PowerShell tooinstall Olá extensão do SQL Server IaaS Agent e configurar seus serviços associados. Saudação de uso **AzureVMSqlServerExtension conjunto** extensão de saudação de tooinstall de cmdlet do PowerShell. Por exemplo, hello comando a seguir instala a extensão de saudação em uma VM do Windows Server (clássico) e nomeia "SQLIaaSExtension".

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Se você atualizar a versão mais recente toohello de saudação extensão do agente SQL IaaS, você deve reiniciar a máquina virtual após a atualização da extensão Olá.

> [!NOTE]
> Máquinas virtuais clássicas não têm uma opção tooinstall e configurar Olá extensão do agente SQL IaaS por meio do portal hello.
> 
> 

## <a name="status"></a>Status
Tooverify unidirecional que extensão hello está instalado é o status do agente de saudação tooview no hello Portal do Azure. Selecione uma máquina virtual listada na folha da máquina virtual hello e, em seguida, clique em **extensões**. Você deve ver Olá **SQLIaaSAgent** extensão listado.

![Extensão do Agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

Você também pode usar o hello **AzureVMSqlServerExtension Get** cmdlet do Powershell do Azure.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Remoção
Olá Portal do Azure, você pode desinstalar extensão Olá clicando reticências Olá em Olá **extensões** folha de propriedades de sua máquina virtual. Em seguida, clique em **Desinstalar**.

![Desinstalar Olá extensão do agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

Você também pode usar o hello **AzureVMSqlServerExtension remover** cmdlet do Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Próximas etapas
Começar a usar um dos serviços de Olá Olá extensão oferece suportados. Para obter mais detalhes, consulte os tópicos de saudação referenciados no hello [suporte para serviços](#supported-services) deste artigo.

Para obter mais informações sobre como executar o SQL Server em Máquinas Virtuais do Azure, veja [Visão geral do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

