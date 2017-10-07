---
title: "aaaAutomated v2 de Backup para máquinas de virtuais do SQL Server 2016 do Azure | Microsoft Docs"
description: "Explica o recurso de Backup automatizado Olá para VMs do SQL Server 2016 em execução no Azure. Este artigo é específico tooVMs usando Olá Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Backup Automatizado v2 para máquinas virtuais do Azure do SQL Server 2016 (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

V2 de Backup automatizado configura automaticamente [tooMicrosoft de Backup gerenciado do Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todos os novos e existentes bancos de dados em uma VM do Azure que executam edições do SQL Server 2016 Standard, Enterprise ou Developer. Isso permite que os backups de banco de dados regular tooconfigure que utilizam o armazenamento de BLOBs do Azure durável. V2 de Backup automatizado depende Olá [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
toouse v2 de Backup automatizado, Olá examine os pré-requisitos a seguir:

**Sistema operacional**:

- Windows Server 2012 R2
- Windows Server 2016

**Versão/edição do SQL Server**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> O Backup Automatizado v2 funciona com o SQL Server 2016. Se você estiver usando o SQL Server 2014, você pode usar o Backup automatizado v1 tooback backup de seus bancos de dados. Para obter mais informações, veja [Backup Automatizado para máquinas virtuais do Azure no SQL Server 2014](virtual-machines-windows-sql-automated-backup.md).

**Configuração do banco de dados**:

- Bancos de dados de destino devem usar o modelo de recuperação completa de saudação. Para obter mais informações sobre o impacto de saudação do modelo de recuperação completa de saudação em backups, consulte [Olá Backup no modelo de recuperação completa](https://technet.microsoft.com/library/ms190217.aspx).
- Bancos de dados do sistema não tem toouse modelo de recuperação completa. No entanto, se você precisar toobe de backups de log levado para o modelo ou MSDB, você deve usar o modelo de recuperação completa.
- Bancos de dados de destino devem estar na instância do SQL Server padrão hello. Olá extensão de IaaS do SQL Server não oferece suporte a instâncias nomeadas.

**Modelo de implantação do Azure**:

- Gerenciador de Recursos

> [!NOTE]
> Backup automatizado depende Olá **extensão do SQL Server IaaS Agent**. As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão. Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Configurações
Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para Backup automatizado v2. etapas de configuração real de saudação variam dependendo se você usar Olá portal do Azure ou comandos do PowerShell do Windows Azure.

### <a name="basic-settings"></a>Configurações Básicas

| Configuração | Intervalo (Padrão) | Descrição |
| --- | --- | --- |
| **Backup Automatizado** | Habilitar/desabilitar (Desabilitado) | Habilita ou desabilita o Backup Automatizado de uma VM do Azure que executa o SQL Server 2016 Standard ou Enterprise. |
| **Período de retenção** | Um a 30 dias (30 dias) | número de saudação de backups de tooretain dias. |
| **Conta de armazenamento** | Conta de Armazenamento do Azure | Um toouse de conta de armazenamento do Azure para armazenar arquivos de Backup automatizado no armazenamento de blob. Um contêiner é criado neste local toostore todos os arquivos de backup. o arquivo de backup Olá convenção de nomenclatura inclui Olá data, hora e GUID do banco de dados. |
| **Criptografia** |Habilitar/desabilitar (Desabilitado) | Habilita ou desabilita a criptografia. Quando a criptografia está habilitada, Olá certificados usados toorestore Olá backup estão localizados em Olá especificado conta de armazenamento em Olá mesmo **automaticbackup** Olá contêiner usando a mesma convenção de nomenclatura. Se Olá senha for alterada, um novo certificado será gerado com essa senha, mas o certificado antigo Olá permanece backups anteriores toorestore. |
| **Senha** |Texto da senha | Uma senha para as chaves de criptografia. Isso só é necessário se a criptografia estiver habilitada. Ordem toorestore um backup criptografado, você deve ter senha correta hello e o certificado relacionado que foi usado em tempo de Olá Olá backup foi feito. |

### <a name="advanced-settings"></a>Configurações avançadas

| Configuração | Intervalo (Padrão) | Descrição |
| --- | --- | --- |
| **Backups de Banco de Dados do Sistema** | Habilitar/desabilitar (Desabilitado) | Quando habilitado, esse recurso também fará backup Olá os bancos de dados: Master, MSDB e modelo. Olá MSDB e bancos de dados de modelo, verifique se eles são no modo de recuperação completa se você quiser toobe de backups de log feito. Os backups de log nunca são feitos para o Mestre. E não é feito nenhum backup para o TempDB. |
| **Agendamento de Backup** | Manual/Automatizado (Automatizado) | Por padrão, o agendamento de backup Olá será automaticamente determinado com base no crescimento do log hello. Agendamento de backup manual permite que a janela de tempo de saudação do hello usuário toospecify para backups. Nesse caso, os backups só terá ocorre na saudação especificado frequência e durante a saudação especificado na janela de tempo de um determinado dia. |
| **Frequência do backup completo** | Diariamente/Semanalmente | Frequência de backups completos. Em ambos os casos, backups completos serão iniciado durante a próxima janela de tempo agendado hello. Quando Semanalmente estiver selecionado, os backups poderão abranger vários dias até que todos os bancos de dados tenham o backup realizado com êxito. |
| **Hora de início do backup completo** | 00:00 – 23:00 (01:00) | A hora de início de um determinado dia durante o qual os backups completos podem ocorrer. |
| **Janela de tempo do backup completo** | 1 – 23 horas (1 hora) | Duração da janela de tempo de saudação de um determinado dia durante o qual os backups completos podem ocorrer. |
| **Frequência de backup do log** | 5 – 60 minutos (60 minutos) | Frequência de backups de log. |

## <a name="understanding-full-backup-frequency"></a>Noções básicas sobre a frequência do backup completo
É importante toounderstand diferença de saudação entre backups completos diários e semanais. Nesse esforço, abordaremos dois cenários de exemplo.

### <a name="scenario-1-weekly-backups"></a>Cenário 1: backups semanais
Você tem uma VM do SQL Server que contém um número de bancos de dados muito grandes.

Na segunda-feira, habilitar o Backup automatizado v2 com hello configurações a seguir:

- Agendamento de backup: **Manual**
- Frequência do backup completo: **Semanalmente**
- Hora de início do backup completo: **01:00**
- Janela de tempo do backup completo: **1 hora**

Isso significa que essa janela de backup disponíveis próxima da saudação é terça-feira à 1H00 por 1 hora. Nesse momento, o Backup Automatizado começará a fazer backup de seus bancos de dados um de cada vez. Nesse cenário, seus bancos de dados são grandes o suficiente para que os backups completos serão concluído para Olá primeiro alguns bancos de dados. No entanto, após uma hora nem todos os bancos de dados Olá tem sido feitos backup.

Quando isso acontece, o Backup automatizado começará a backup Olá restantes Olá bancos de dados dia seguinte, quarta-feira à 1H00 por 1 hora. Se nem todos os bancos de dados tem sido feitos no momento, ele tentará novamente Olá próximo dia no hello mesmo tempo. Isso continuará até que todos os bancos de dados tenham tido o backup realizado com êxito.

Quando chegar terça-feira novamente, o Backup Automatizado começará a fazer o backup de todos os bancos de dados novamente.

Este cenário mostra que o Backup automatizado só funciona dentro da janela de tempo especificada Olá, e cada banco de dados será feito uma vez por semana. Isso também mostra que é possível para backups toospan vários dias no hello caso onde não é possível toocomplete todos os backups em um único dia.

### <a name="scenario-2-daily-backups"></a>Cenário 2: backups diários
Você tem uma VM do SQL Server que contém um número de bancos de dados muito grandes.

Na segunda-feira, habilitar o Backup automatizado v2 com hello configurações a seguir:

- Agendamento de backup: Manual
- Frequência do backup completo: Diariamente
- Hora de início do backup completo: 22:00
- Janela de tempo do backup completo: 6 horas

Isso significa que essa janela de backup disponíveis próxima da saudação é segunda-feira às 10 PM para 6 horas. Nesse momento, o Backup Automatizado começará a fazer backup de seus bancos de dados um de cada vez.

Em seguida, na terça-feira às 22h por 6 horas, os backups completos de todos os bancos de dados serão iniciados novamente.

> [!IMPORTANT]
> Quando o agendamento de backups diários, é recomendável que você agende uma tooensure de janela de tempo ampla todos os bancos de dados podem ser feitos no momento. Isso é especialmente importante no caso de Olá onde você tem uma grande quantidade de dados tooback backup.

## <a name="configuration-in-hello-portal"></a>Configuração no Portal de saudação

Você pode usar o hello tooconfigure portal do Azure Backup automatizado v2 durante o provisionamento ou para VMs existentes do SQL Server 2016.

### <a name="new-vms"></a>Novas VMs

Use Olá tooconfigure portal do Azure Backup automatizado v2 quando você cria uma nova máquina SQL Server 2016 Virtual no modelo de implantação do Gerenciador de recursos de saudação. 

Em Olá **configurações do SQL Server** folha, selecione **backup automatizado**. Olá, seguinte captura de tela de portal do Azure mostra Olá **Backup automatizado do SQL** folha.

![Configuração de Backup Automatizado do SQL no portal do Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> O Backup Automatizado v2 está desabilitado por padrão.

Para o contexto, consulte o tópico completo do hello sobre [Provisionando uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VMs existentes

Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server. Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.

![Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

Em hello **configuração do SQL Server** folha, clique em hello **editar** botão Olá automatizada seção de backup.

![Configurar o Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.

Se você estiver habilitando o Backup automatizado para Olá primeira vez, o Azure configura Olá IaaS do SQL Server Agent no plano de fundo de saudação. Durante esse tempo, Olá portal do Azure não pode mostrar que o Backup automatizado é configurado. Aguarde alguns minutos para Olá agente toobe instalado, configurado. Depois que hello Azure portal refletirá novas configurações de saudação.

## <a name="configuration-with-powershell"></a>Configuração com o PowerShell

Você pode usar o PowerShell tooconfigure v2 de Backup automatizado. Antes de começar, faça o seguinte:

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
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Se a saída mostra que **habilitar** está definido muito**False**, em seguida, você tem o backup automatizado tooenable. Olá boa notícia é que você habilita e configurar o Backup automatizado no hello mesma maneira. Consulte a próxima seção Olá para obter essas informações.

> [!NOTE] 
> Se você verificar as configurações de saudação imediatamente depois de fazer uma alteração, é possível que você receberá novamente os valores de configuração antigo hello. Aguarde alguns minutos e verificar as configurações de saudação novamente toomake-se de que as alterações foram aplicadas.

### <a name="configure-automated-backup-v2"></a>Configurar o Backup Automatizado v2
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

Em seguida, usar o hello **AzureRmVMSqlServerAutoBackupConfig novo** tooenable de comando e configurar backups de toostore configurações Olá Backup automatizado v2 na conta de armazenamento do Azure hello. Neste exemplo, os backups de saudação são definidos toobe mantido por 10 dias. Os backups de banco de dados do sistema estão habilitados. Os backups completos são agendados para serem realizados semanalmente com uma janela de tempo com início às 20h por duas horas. Os backups de log estão agendados para a cada 30 minutos. Olá o segundo comando, **AzureRmVMSqlServerExtension conjunto**, Olá atualizações especificado VM do Azure com essas configurações.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent. 

criptografia de tooenable modificar Olá Olá de toopass script anterior **EnableEncryption** parâmetro junto com uma senha (cadeia de caracteres segura) para Olá **CertificatePassword** parâmetro. Olá script a seguir permite que as configurações de Backup automatizado Olá no exemplo anterior hello e adiciona a criptografia.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

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
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Próximas etapas
O Backup Automatizado v2 configura o Backup Gerenciado em VMs do Azure. Portanto, é muito importante[documentação Olá Backup gerenciado](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Olá comportamento e as implicações.

Você pode encontrar backup adicional e restaurar a orientação do SQL Server em VMs do Azure no hello tópico a seguir: [de Backup e restauração do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-backup-recovery.md).

Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).

