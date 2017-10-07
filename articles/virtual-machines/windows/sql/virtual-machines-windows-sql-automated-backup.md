---
title: "aaaAutomated Backup para máquinas de virtuais do SQL Server 2014 do Azure | Microsoft Docs"
description: "Explica o recurso de Backup automatizado Olá para VMs do SQL Server 2014 em execução no Azure. Este artigo é específico tooVMs usando Olá Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>Backup Automatizado para em máquinas virtuais do SQL Server 2014 (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Backup automatizado configura automaticamente [tooMicrosoft de Backup gerenciado do Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todos os novos e existentes bancos de dados em uma VM do Azure executando o SQL Server 2014 Standard ou Enterprise. Isso permite que os backups de banco de dados regular tooconfigure que utilizam o armazenamento de BLOBs do Azure durável. Backup automatizado depende Olá [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
toouse Backup automatizado, considere Olá pré-requisitos a seguir:

**Sistema operacional**:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**Versão/edição do SQL Server**:

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> O Backup Automatizado funciona com o SQL Server 2014. Se você estiver usando o SQL Server 2016, você pode usar o Backup automatizado v2 tooback backup de seus bancos de dados. Para saber mais, confira [Backup Automatizado v2 para máquinas virtuais do Azure no SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).

**Configuração do banco de dados**:

- Bancos de dados de destino devem usar o modelo de recuperação completa de saudação. Para obter mais informações sobre o impacto de saudação do modelo de recuperação completa de saudação em backups, consulte [Olá Backup no modelo de recuperação completa](https://technet.microsoft.com/library/ms190217.aspx).
- Bancos de dados de destino devem estar na instância do SQL Server padrão hello. Olá extensão de IaaS do SQL Server não oferece suporte a instâncias nomeadas.

**Modelo de implantação do Azure**:

- Gerenciador de Recursos

**Azure PowerShell**:

- [Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview) se você planejar tooconfigure Backup automatizado com o PowerShell.

> [!NOTE]
> Backup automatizado depende Olá extensão do SQL Server IaaS Agent. As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão. Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Configurações

Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para Backup automatizado. etapas de configuração real de saudação variam dependendo se você usar Olá portal do Azure ou comandos do PowerShell do Windows Azure.

| Configuração | Intervalo (Padrão) | Descrição |
| --- | --- | --- |
| **Backup Automatizado** | Habilitar/desabilitar (Desabilitado) | Habilita ou desabilita o Backup Automatizado de uma VM do Azure que executa o SQL Server 2014 Standard ou Enterprise. |
| **Período de retenção** | Um a 30 dias (30 dias) | número de saudação de dias tooretain um backup. |
| **Conta de armazenamento** | Conta de Armazenamento do Azure | Um toouse de conta de armazenamento do Azure para armazenar arquivos de Backup automatizado no armazenamento de blob. Um contêiner é criado neste local toostore todos os arquivos de backup. o arquivo de backup Olá convenção de nomenclatura inclui Olá data, hora e nome do computador. |
| **Criptografia** | Habilitar/desabilitar (Desabilitado) | Habilita ou desabilita a criptografia. Quando a criptografia está habilitada, Olá certificados usados toorestore Olá backup estão localizados em Olá especificado conta de armazenamento em Olá mesmo `automaticbackup` Olá contêiner usando a mesma convenção de nomenclatura. Se Olá senha for alterada, um novo certificado será gerado com essa senha, mas o certificado antigo Olá permanece backups anteriores toorestore. |
| **Senha** | Texto da senha | Uma senha para as chaves de criptografia. Isso só é necessário se a criptografia estiver habilitada. Ordem toorestore um backup criptografado, você deve ter senha correta hello e o certificado relacionado que foi usado em tempo de Olá Olá backup foi feito. |

## <a name="configuration-in-hello-portal"></a>Configuração no Portal de saudação

Você pode usar o hello tooconfigure portal do Azure Backup automatizado durante o provisionamento ou para VMs existentes do SQL Server 2014.

### <a name="new-vms"></a>Novas VMs

Use Olá tooconfigure portal do Azure Backup automatizado quando você cria uma nova máquina SQL Server 2014 Virtual no modelo de implantação do Gerenciador de recursos de saudação.

Em Olá **configurações do SQL Server** folha, selecione **backup automatizado**. Olá, seguinte captura de tela de portal do Azure mostra Olá **Backup automatizado do SQL** folha.

![Configuração de Backup Automatizado do SQL no portal do Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

Para o contexto, consulte o tópico completo do hello sobre [Provisionando uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VMs existentes

Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server. Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.

![Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

Em hello **configuração do SQL Server** folha, clique em hello **editar** botão Olá automatizada seção de backup.

![Configurar o Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.

Se você estiver habilitando o Backup automatizado para Olá primeira vez, o Azure configura Olá IaaS do SQL Server Agent no plano de fundo de saudação. Durante esse tempo, Olá portal do Azure não pode mostrar que o Backup automatizado é configurado. Aguarde alguns minutos para Olá agente toobe instalado, configurado. Depois que hello Azure portal refletirá novas configurações de saudação.

> [!NOTE]
> Você também pode configurar o Backup Automatizado usando um modelo. Para obter mais informações, consulte o [Modelo de início rápido do Azure para o Backup Automatizado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).

## <a name="configuration-with-powershell"></a>Configuração com o PowerShell

Você pode usar o PowerShell tooconfigure Backup automatizado. Antes de começar, faça o seguinte:

- [Baixe e instale o hello Azure PowerShell mais recente](http://aka.ms/webpi-azps).
- Abra o Windows PowerShell e associe-o à sua conta. Você pode fazer isso, seguindo as etapas de Olá Olá [configurar sua assinatura](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) seção Olá provisionamento tópico.

### <a name="install-hello-sql-iaas-extension"></a>Instalar Olá extensão SQL IaaS
Se você provisionar uma máquina de virtual do SQL Server do hello portal do Azure, Olá extensão de IaaS do SQL Server já deve ser instalado. Você pode determinar se ele é instalado em sua VM chamando **Get-AzureRmVM** comando e examinando Olá **extensões** propriedade.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

Se Olá extensão do SQL Server IaaS Agent estiver instalado, você verá que ele listado como "SqlIaaSAgent" ou "SQLIaaSExtension". **ProvisioningState** para extensão Olá também deve mostrar "Êxito".

Se ele não está instalado ou com falha toobe provisionado, você pode instalá-lo com hello comando a seguir. Adição toohello VM nome e grupo de recursos, você deve também especificar região hello (**$region**) localizado na sua VM.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <a id="verifysettings"></a> Verificar as configurações atuais

Se você habilitou o backup automatizado durante o provisionamento, você pode usar PowerShell toocheck sua configuração atual. Executar Olá **Get-AzureRmVMSqlServerExtension** de comando e examine Olá **AutoBackupSettings** propriedade:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

Você deve obter a seguir toohello semelhante saída:

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

Se a saída mostra que **habilitar** está definido muito**False**, em seguida, você tem o backup automatizado tooenable. Olá boa notícia é que você habilita e configurar o Backup automatizado no hello mesma maneira. Consulte a próxima seção Olá para obter essas informações.

> [!NOTE] 
> Se você verificar as configurações de saudação imediatamente depois de fazer uma alteração, é possível que você receberá novamente os valores de configuração antigo hello. Aguarde alguns minutos e verificar as configurações de saudação novamente toomake-se de que as alterações foram aplicadas.

### <a name="configure-automated-backup"></a>Configurar o Backup Automatizado
Você pode usar PowerShell tooenable Backup automatizado, bem como toomodify sua configuração e o comportamento a qualquer momento.

Primeiro, selecione ou crie uma conta de armazenamento para Olá arquivos de backup. Olá script a seguir seleciona uma conta de armazenamento ou cria se ele não existe.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> O Backup Automatizado não dá suporte ao armazenamento de backups no Armazenamento Premium, mas ele pode fazer backups de discos de VM que usam o Armazenamento Premium.

Em seguida, usar Olá **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de comando e configurar backups de toostore de configurações de Backup automatizado de saudação em Olá conta de armazenamento do Azure. Neste exemplo, os backups de saudação são definidos toobe mantido por 10 dias. Olá o segundo comando, **AzureRmVMSqlServerExtension conjunto**, Olá atualizações especificado VM do Azure com essas configurações.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.

> [!NOTE]
> Existem outras configurações para **AzureRmVMSqlServerAutoBackupConfig novo** que se aplicam somente tooSQL Server 2016 e Backup automatizado v2. SQL Server 2014 não oferece suporte a saudação configurações a seguir: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, e **LogBackupFrequencyInMinutes**. Se você tentar tooconfigure essas configurações em uma máquina de virtual do SQL Server 2014, nenhum erro, mas as configurações de saudação não serão aplicadas. Se você quiser que essas configurações em uma máquina de virtual do SQL Server 2016 toouse, consulte [v2 de Backup automatizado para máquinas de virtuais do SQL Server 2016 Azure](virtual-machines-windows-sql-automated-backup-v2.md).

criptografia de tooenable modificar Olá Olá de toopass script anterior **EnableEncryption** parâmetro junto com uma senha (cadeia de caracteres segura) para Olá **CertificatePassword** parâmetro. Olá script a seguir permite que as configurações de Backup automatizado Olá no exemplo anterior hello e adiciona a criptografia.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

tooconfirm suas configurações são aplicadas, [verificar a configuração de Backup automatizado Olá](#verifysettings).

### <a name="disable-automated-backup"></a>Desabilitar o Backup automatizado

toodisable Backup automatizado, Olá execução mesmo script sem Olá **-habilitar** parâmetro toohello **AzureRmVMSqlServerAutoBackupConfig novo** comando. Olá ausência de saudação **-habilitar** recurso de saudação do parâmetro sinais Olá comando toodisable. Como com a instalação, pode levar vários minutos toodisable Backup automatizado.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Script de exemplo

Olá script a seguir fornece um conjunto de variáveis que você pode personalizar tooenable e configurar o Backup automatizado para sua VM. No seu caso, talvez seja necessário toocustomize script de saudação com base nos seus requisitos. Por exemplo, você deve ter toomake alterações se desejar que o backup de saudação toodisable de bancos de dados do sistema ou habilitar a criptografia.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Próximas etapas

O Backup Automatizado configura o Backup Gerenciado em VMs do Azure. Portanto, é muito importante[documentação Olá Backup gerenciado](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Olá comportamento e as implicações.

Você pode encontrar backup adicional e restaurar a orientação do SQL Server em VMs do Azure no hello tópico a seguir: [de Backup e restauração do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-backup-recovery.md).

Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).

