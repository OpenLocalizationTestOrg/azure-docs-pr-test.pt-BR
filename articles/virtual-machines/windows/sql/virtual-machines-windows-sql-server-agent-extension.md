---
title: tarefas de gerenciamento de aaaAutomate em VMs do SQL (Gerenciador de recursos) | Microsoft Docs
description: "Este tópico descreve como toomanage Olá extensão do agente do SQL Server, que automatiza tarefas de administração do SQL Server específicas. Entre elas estão o Backup Automatizado, a Aplicação de Patch Automatizada e a Integração do Cofre de Chaves do Azure. Este tópico usa o modo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Automatizar tarefas de gerenciamento em máquinas virtuais do Azure com hello extensão do SQL Server Agent (Gerenciador de recursos)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](virtual-machines-windows-sql-server-agent-extension.md)
> * [Clássico](../classic/sql-server-agent-extension.md)
> 
> 

Olá extensão do agente IaaS do SQL Server (SQLIaaSExtension) é executado em máquinas virtuais do Azure tooautomate as tarefas de administração. Este tópico fornece uma visão geral dos serviços de saudação suportados pela extensão de hello, bem como instruções de instalação, status e remoção.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview Olá clássico versão deste artigo, consulte [extensão do agente do SQL Server para SQL Server VMs clássico](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Serviços com suporte
Olá extensão do SQL Server IaaS Agent dá suporte a saudação tarefas de administração a seguir:

| Recurso de administração | Descrição |
| --- | --- |
| **Backup Automatizado do SQL** |Automatiza Olá agendamento de backups para todos os bancos de dados para instância padrão de saudação do SQL Server na VM de saudação. Para saber mais, veja [Backup automatizado para SQL Server em máquinas virtuais do Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md). |
| **Aplicação de patch automatizada do SQL** |Configura uma janela de manutenção durante as atualizações tooyour VM pode levar coloca, para que você possa evitar atualizações durante horários de pico para sua carga de trabalho. Para saber mais, veja [Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md). |
| **Integração do Cofre da Chave do Azure** |Permite que você tooautomatically instalar e configurar o Cofre de chaves do Azure na VM do SQL Server. Para saber mais, confira [Configurar a integração do Cofre de Chaves do Azure para SQL Server em VMs do Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md). |

Depois de instalado e em execução, Olá extensão do SQL Server IaaS Agent disponibiliza esses recursos de administração no painel de SQL Server de saudação do hello máquina virtual no hello Portal do Azure e por meio do PowerShell do Azure para imagens do marketplace do SQL Server e por meio de Azure PowerShell para instalações manuais de extensão de saudação. 

## <a name="prerequisites"></a>Pré-requisitos
Requisitos toouse Olá extensão do SQL Server IaaS Agent na sua VM:

**Sistema operacional**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versões do SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Baixar e configurar os comandos do PowerShell do Azure mais recentes Olá](/powershell/azure/overview)

## <a name="installation"></a>Instalação
Olá extensão do SQL Server IaaS Agent é instalado automaticamente quando você provisiona uma das imagens de galeria de máquina virtual saudação do SQL Server. Se você precisar de extensão de saudação tooreinstall manualmente em um dessas VMs do SQL Server, use Olá comando PowerShell a seguir:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

Também é possível tooinstall Olá extensão do SQL Server IaaS Agent em uma máquina virtual de somente do sistema operacional Windows Server. Isso será suportado apenas se você tiver instalado manualmente o SQL Server nesta máquina. Em seguida, instalar Olá extensão manualmente usando Olá mesmo **AzureVMSqlServerExtension conjunto** cmdlet do PowerShell.

> [!NOTE]
> Se você instalar manualmente o hello extensão do SQL Server IaaS Agent em uma VM somente do sistema operacional Windows Server, você não pode gerenciar as definições de configuração do SQL Server Olá por meio de saudação portal do Azure. Nesse cenário, você deverá fazer todas as alterações com o PowerShell.

## <a name="status"></a>Status
Tooverify unidirecional que extensão hello está instalado é o status do agente de saudação tooview no hello Portal do Azure. Selecione **todas as configurações** Olá folha da máquina virtual e, em seguida, clique em **extensões**. Você deve ver Olá **SQLIaaSExtension** extensão listado.

![Extensão do Agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

Você também pode usar o hello **AzureVMSqlServerExtension Get** cmdlet do Powershell do Azure.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

comando anterior Olá confirma agente hello está instalado e fornece informações de status geral. Você também pode obter informações de status específicas sobre o Backup automatizado e aplicação de patch com hello comandos a seguir.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Remoção
Olá Portal do Azure, você pode desinstalar extensão Olá clicando reticências Olá em Olá **extensões** folha de propriedades de sua máquina virtual. Em seguida, clique em **Excluir**.

![Desinstalar Olá extensão do agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

Você também pode usar o hello **AzureRmVMSqlServerExtension remover** cmdlet do Powershell.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Próximas etapas
Começar a usar um dos serviços de Olá Olá extensão oferece suportados. Para obter mais detalhes, consulte os tópicos de saudação referenciados no hello [suporte para serviços](#supported-services) deste artigo.

Para obter mais informações sobre como executar o SQL Server em Máquinas Virtuais do Azure, veja [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).

