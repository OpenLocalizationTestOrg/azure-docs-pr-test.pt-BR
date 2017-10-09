---
title: "aaaAutomated Backup para máquinas de virtuais de servidor do SQL (clássico) | Microsoft Docs"
description: "Explica o recurso de Backup automatizado Olá para SQL Server em execução em máquinas virtuais do Azure usando o Gerenciador de recursos. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Backup automatizado para SQL Server em Máquinas Virtuais do Azure (Clássico)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Clássico](../classic/sql-automated-backup.md)
> 
> 

Backup automatizado configura automaticamente [tooMicrosoft de Backup gerenciado do Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todos os novos e existentes bancos de dados em uma VM do Azure executando o SQL Server 2014 Standard ou Enterprise. Isso permite que os backups de banco de dados regular tooconfigure que utilizam o armazenamento de BLOBs do Azure durável. Backup automatizado depende Olá [extensão do SQL Server IaaS Agent](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. versão do Gerenciador de recursos de saudação tooview deste artigo, consulte [Backup automatizado para SQL Server no Gerenciador de recursos de máquinas virtuais do Azure](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Pré-requisitos
toouse Backup automatizado, considere Olá pré-requisitos a seguir:

**Sistema operacional**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versão/edição do SQL Server**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> No Backup Automatizado, ainda não há suporte para o SQL Server 2016.
> 
> 

**Configuração do banco de dados**:

* Bancos de dados de destino devem usar o modelo de recuperação completa de saudação.

**Azure PowerShell**:

* [Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview).

**Extensão IaaS do SQL Server**:

* [Instalar Olá extensão do SQL Server IaaS](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Configurações
Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para Backup automatizado. Para VMs clássicas, você deve usar PowerShell tooconfigure essas configurações.

| Configuração | Intervalo (Padrão) | Descrição |
| --- | --- | --- |
| **Backup Automatizado** |Habilitar/desabilitar (Desabilitado) |Habilita ou desabilita o Backup Automatizado de uma VM do Azure que executa o SQL Server 2014 Standard ou Enterprise. |
| **Período de retenção** |Um a 30 dias (30 dias) |número de saudação de dias tooretain um backup. |
| **Conta de armazenamento** |Conta de armazenamento do Azure (conta de armazenamento Olá criada para Olá especificado VM) |Um toouse de conta de armazenamento do Azure para armazenar arquivos de Backup automatizado no armazenamento de blob. Um contêiner é criado neste local toostore todos os arquivos de backup. o arquivo de backup Olá convenção de nomenclatura inclui Olá data, hora e nome do computador. |
| **Criptografia** |Habilitar/desabilitar (Desabilitado) |Habilita ou desabilita a criptografia. Quando a criptografia está habilitada, certificados Olá backup de saudação toorestore usados estão localizados em Olá especificado conta de armazenamento no hello automaticbackup mesmo contêiner usando Olá a mesma convenção de nomenclatura. Se Olá senha for alterada, um novo certificado será gerado com essa senha, mas o certificado antigo Olá permanece backups anteriores toorestore. |
| **Senha** |Texto da senha (nenhum) |Uma senha para as chaves de criptografia. Isso só é necessário se a criptografia estiver habilitada. Ordem toorestore um backup criptografado, você deve ter senha correta hello e o certificado relacionado que foi usado em tempo de Olá Olá backup foi feito. | **Bancos de dados do sistema de backup** | Habilitar/desabilitar (Desabilitado) | Fazer backups completos do Mestre, Modelo e MSDB |
| **Configurar agendamento de backup** | Manual/Automatizado (Automatizado) | Selecione **automatizada** tooautomatically levar completa e com base no crescimento do log de backups de log. Selecione **Manual** toospecify agenda de saudação para completo e backups de log. |

## <a name="configuration-with-powershell"></a>Configuração com o PowerShell
Olá PowerShell de exemplo a seguir, o Backup automatizado é configurado para uma VM existente do SQL Server 2014. Olá **AzureVMSqlServerAutoBackupConfig novo** comando configura os backups de toostore de configurações de Backup automatizado Olá na conta de armazenamento do Azure Olá especificada pela variável Olá $storageaccount. Esses backups serão mantidos por 10 dias. Olá **AzureVMSqlServerExtension conjunto** comando Olá atualizações especificado VM do Azure com essas configurações.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.

criptografia de tooenable modificar Olá anterior script toopass Olá parâmetro EnableEncryption junto com uma senha (cadeia de caracteres segura) para o parâmetro CertificatePassword de saudação. Olá script a seguir permite que as configurações de Backup automatizado Olá no exemplo anterior hello e adiciona a criptografia.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

toodisable o backup automático, Olá execução mesmo script sem Olá **-habilitar** parâmetro toohello **AzureVMSqlServerAutoBackupConfig novo**. Como com a instalação, pode levar vários minutos toodisable Backup automatizado.

> [!NOTE]
> Desabilitar e desinstalar Olá IaaS do SQL Server Agent não remove as configurações de Backup gerenciado Olá configurado anteriormente. Você deve desabilitar o Backup automatizado antes de desabilitar ou desinstalar Olá SQL Server IaaS Agent.
> 
> 

## <a name="next-steps"></a>Próximas etapas
O Backup Automatizado configura o Backup Gerenciado em VMs do Azure. Portanto, é muito importante[documentação Olá Backup gerenciado](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Olá comportamento e as implicações.

Você pode encontrar backup adicional e restaurar a orientação do SQL Server em VMs do Azure no hello tópico a seguir: [de Backup e restauração do SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](../classic/sql-server-agent-extension.md).

Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

