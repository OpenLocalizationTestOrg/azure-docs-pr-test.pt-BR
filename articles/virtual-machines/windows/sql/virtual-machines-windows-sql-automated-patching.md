---
title: "aaaAutomated aplicação de patches para VMs do SQL Server (Gerenciador de recursos) | Microsoft Docs"
description: "Explica o recurso de aplicação de patch automatizada hello para SQL Server máquinas virtuais em execução no Azure usando o Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Gerenciador de Recursos)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](virtual-machines-windows-sql-automated-patching.md)
> * [Clássico](../classic/sql-automated-patching.md)
> 
> 

A aplicação de patch automatizada estabelece uma janela de manutenção para uma Máquina Virtual do Azure que executa o SQL Server. Atualizações automáticas só podem ser instaladas durante esta janela de manutenção. Para o SQL Server, esse rescriction garante que as atualizações do sistema e qualquer reinicialização associada ocorre no melhor tempo possível Olá para o banco de dados de saudação. Aplicação de patch automatizada depende Olá [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview Olá clássico versão deste artigo, consulte [aplicação de patch automatizada para SQL Server no Azure máquinas virtuais clássicas](../classic/sql-automated-patching.md).

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

* [Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview) se você planejar tooconfigure aplicação de patch automatizada com o PowerShell.

> [!NOTE]
> Aplicação de patch automatizada depende Olá extensão do SQL Server IaaS Agent. As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão. Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).
> 
> 

## <a name="settings"></a>Configurações
Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para aplicação de patch automatizada. etapas de configuração real de saudação variam dependendo se você usar Olá portal do Azure ou comandos do PowerShell do Windows Azure.

| Configuração | Valores possíveis | Descrição |
| --- | --- | --- |
| **Aplicação de patch automatizada** |Habilitar/desabilitar (Desabilitado) |Habilita ou desabilita a Aplicação de Patch Automatizada para uma máquina virtual do Azure. |
| **Agenda de manutenção** |Todos os dias, segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira, sábado e domingo |agenda de saudação para baixar e instalar atualizações do Windows, SQL Server e Microsoft para sua máquina virtual. |
| **Hora de início da manutenção** |0h a 24h |Olá início local tempo tooupdate Olá VM. |
| **Duração da janela de manutenção** |30-180 |número de saudação de minutos permitidos download de saudação toocomplete e instalação de atualizações. |
| **Categoria de patch** |Importante |categoria de saudação do toodownload atualizações e instalar. |

## <a name="configuration-in-hello-portal"></a>Configuração no Portal de saudação
Você pode usar o hello tooconfigure portal do Azure aplicação de patch automatizada durante o provisionamento ou para máquinas virtuais existentes.

### <a name="new-vms"></a>Novas VMs
Saudação de uso do Azure tooconfigure portal aplicação de patch automatizada quando você cria uma nova máquina Virtual do SQL Server no modelo de implantação do Gerenciador de recursos de saudação.

Em Olá **configurações do SQL Server** folha, selecione **aplicação de patches automatizada**. Olá, seguinte captura de tela de portal do Azure mostra Olá **SQL Automated Patching** folha.

![Aplicação de Patch Automática do SQL no Portal do Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Para o contexto, consulte o tópico completo do hello sobre [Provisionando uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VMs existentes
Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server. Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.

![Aplicação de Patch Automática do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

Em Olá **configuração do SQL Server** folha, clique em Olá **editar** botão Olá automatizada seção aplicação de patch.

![Configurar a Aplicação de Patch Automática do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.

Se você estiver habilitando aplicação de patch automatizada para Olá primeira vez, o Azure configura Olá IaaS do SQL Server Agent no plano de fundo de saudação. Durante esse tempo, Olá portal do Azure não pode mostrar que a aplicação de patch automatizada está configurada. Aguarde alguns minutos para Olá agente toobe instalado, configurado. Depois que hello Azure portal reflete novas configurações de saudação.

> [!NOTE]
> Você também pode configurar a Aplicação de Patch Automatizada usando um modelo. Para obter mais informações, consulte o [Modelo de início rápido do Azure para a Aplicação de Patch Automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a>Configuração com o PowerShell
Depois de provisionar a VM do SQL, use PowerShell tooconfigure aplicação de patch automatizada.

Olá exemplo a seguir, PowerShell é usado tooconfigure aplicação de patch automatizada em uma VM existente do SQL Server. Olá **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** comando configura uma nova janela de manutenção para atualizações automáticas.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

Com base neste exemplo, hello tabela a seguir descreve a efeito prático Olá no destino Olá VM do Azure:

| Parâmetro | Efeito |
| --- | --- |
| **DayOfWeek** |Patches instalados toda quinta-feira. |
| **MaintenanceWindowStartingHour** |Inicia as atualizações às 11h. |
| **MaintenanceWindowsDuration** |Os patches devem ser instalados dentro de 120 minutos. Com base na hora de início do hello, elas devem concluir até 1:00 pm. |
| **PatchCategory** |Olá única configuração possível para esse parâmetro é **importante**. |

Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.

toodisable aplicação de patch automatizada, Olá execução mesmo script sem Olá **-habilitar** parâmetro toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**. Olá ausência de saudação **-habilitar** recurso de saudação do parâmetro sinais Olá comando toodisable.

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).

