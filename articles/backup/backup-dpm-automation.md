---
title: aaaAzure Backup - Use o PowerShell tooback cargas de trabalho do DPM | Microsoft Docs
description: Saiba como toodeploy e gerenciar o Backup do Azure para o Data Protection Manager (DPM) usando o PowerShell
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Implantar e gerenciar o backup tooAzure para servidores do Data Protection Manager (DPM) usando o PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Clássico](backup-dpm-automation-classic.md)
>
>

Este artigo mostra como toouse PowerShell toosetup Backup do Azure em um servidor DPM e toomanage backup e recuperação.

## <a name="setting-up-hello-powershell-environment"></a>Configurando o ambiente do PowerShell Olá
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Antes de você pode usar o PowerShell toomanage backups tooAzure Data Protection Manager, é necessário toohave Olá direita ambiente PowerShell. No início de saudação da sessão do PowerShell Olá, certifique-se de que você execute Olá módulos corretos do comando tooimport Olá a seguir e permitem que você toocorrectly Referência Olá DPM cmdlets:

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>Configuração e registro
toobegin:

1. [Baixe o PowerShell mais recente](https://github.com/Azure/azure-powershell/releases) (a versão mínima exigida é: 1.0.0)
2. Habilitar cmdlets do Backup do Azure Olá alternando muito*AzureResourceManager* modo usando Olá **Switch-AzureMode** commandlet:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Olá tarefas de registro e configuração a seguir podem ser automatizadas com o PowerShell:

* Criar um cofre dos Serviços de Recuperação
* Instalando o agente de Backup do Azure Olá
* Registrando Olá serviço Backup do Azure
* Configurações de rede
* Configurações de criptografia

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
Olá etapas levá-lo na criação de um cofre de serviços de recuperação. Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.

1. Se você estiver usando o Backup do Azure para Olá primeira vez, você deve usar o hello **registro AzureRMResourceProvider** provedor de serviço de recuperação do Azure do cmdlet tooregister Olá com sua assinatura.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Olá Cofre de serviços de recuperação é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos. Você pode usar um grupo de recursos existente ou criar um novo. Ao criar um novo grupo de recursos, especifique o nome de saudação e local para o grupo de recursos de saudação.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Saudação de uso **AzureRmRecoveryServicesVault novo** cmdlet toocreate um novo cofre. Certifique-se de que toospecify Olá mesmo local para o cofre Olá que foi usada para o grupo de recursos de saudação.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Especificar o tipo de saudação do toouse de redundância de armazenamento; Você pode usar [armazenamento localmente redundante (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [Geo redundante GRS (armazenamento)](../storage/common/storage-redundancy.md#geo-redundant-storage). Olá exemplo a seguir mostra Olá - BackupStorageRedundancy opção testVault é definida tooGeoRedundant.

   > [!TIP]
   > Muitos cmdlets do Backup do Azure exigem Olá objeto de Cofre de serviços de recuperação como entrada. Por esse motivo, é conveniente toostore Olá serviços de recuperação de Backup cofre objeto em uma variável.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>Exibição Olá cofres em uma assinatura
Use **Get-AzureRmRecoveryServicesVault** tooview lista de saudação de todos os cofres na assinatura atual hello. Você pode usar este toocheck de comando que um novo cofre foi criado ou toosee que cofres estão disponíveis na assinatura de saudação.

Execute o comando hello, Get-AzureRmRecoveryServicesVault, e todos os cofres na assinatura de saudação são listados.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Instalando o agente de Backup do Azure Olá em um servidor DPM
Antes de instalar o agente de Backup do Azure Olá, você precisará instalador de saudação toohave baixado e presente no saudação do Windows Server. Você pode obter a versão mais recente de saudação do instalador de saudação de saudação [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou da página de painel do Cofre de serviços de recuperação hello. Salvar instalador Olá tooan local facilmente acessível, como * C:\Downloads\*.

tooinstall Olá execução do agente, Olá seguinte comando em um console do PowerShell com privilégios elevados **no servidor DPM Olá**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Isso instala o agente de saudação com todas as opções padrão de saudação. instalação de saudação leva alguns minutos no plano de fundo de saudação. Se você não especificar Olá */nu* Olá opção **Windows Update** janela será aberta no final de saudação do hello instalação toocheck para todas as atualizações.

Agente de saudação são mostrados na lista de saudação de programas instalados. lista de saudação toosee de instalado programas, consulte muito**painel de controle** > **programas** > **programas e recursos**.

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opções de instalação
toosee todas as opções de saudação disponíveis por meio de saudação de linha de comando, use Olá a seguir de comando:

```
PS C:\> MARSAgentInstaller.exe /?
```

Olá as opções disponíveis incluem:

| Opção | Detalhes | Padrão |
| --- | --- | --- |
| /q |Instalação silenciosa |- |
| /p:"local" |Pasta de instalação de toohello de caminho para o agente de Backup do Azure hello. |C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent |
| /s:"local" |Pasta de cache de toohello de caminho para o agente de Backup do Azure hello. |C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch |
| /m |Aceitar tooMicrosoft atualização |- |
| /nu |Não verificar se há atualizações após a conclusão da instalação |- |
| /d |Desinstala o agente dos Serviços de Recuperação do Microsoft Azure |- |
| /ph |Endereço do host do proxy |- |
| /po |Número da porta do host do proxy |- |
| /pu |UserName do host do proxy |- |
| /pw |Senha do proxy |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a>Registrando o DPM tooa Cofre de serviços de recuperação
Depois que você criar o Cofre de serviços de recuperação de Olá, baixe o agente mais recente hello e as credenciais do cofre hello e armazená-lo em um local conveniente como C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

No servidor DPM hello, executar Olá [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister Olá máquina cofre hello.

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a>Definições de configuração iniciais
Depois que o hello servidor DPM está registrado com hello Cofre de serviços de recuperação, ele começa com as configurações de assinatura padrão. Essas configurações de assinatura incluem Olá área de preparação, a criptografia e a rede. configurações de assinatura toochange necessário toofirst obtém um identificador nas configurações (padrão) existentes hello usando Olá [DPMCloudSubscriptionSetting Get](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Todas as modificações são feitas toothis local PowerShell objeto ```$setting``` e completa do objeto Olá é confirmada tooDPM e toosave de Backup do Azure-los usando Olá [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet. Você precisa Olá toouse ```–Commit``` tooensure de sinalizador que Olá alterações são mantidas. configurações de saudação não serão aplicadas e usadas pelo Backup do Azure, a menos que confirmada.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a>Rede
Se a conectividade de saudação do hello DPM máquina toohello serviço de Backup do Azure no hello internet for por meio de um servidor proxy, configurações do servidor proxy Olá devem ser fornecidas para os backups bem-sucedidos. Isso é feito usando Olá ```-ProxyServer```e ```-ProxyPort```, ```-ProxyUsername``` e hello ```ProxyPassword``` parâmetros com hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet. Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Uso de largura de banda também pode ser controlado com opções de ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` para um determinado conjunto de dias da semana hello. Neste exemplo, não definimos nenhuma limitação.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a>Configurando a área de preparação de saudação
Hello Azure Backup agent em execução no servidor DPM Olá precisa de armazenamento temporário para os dados restaurados da nuvem de saudação (área de preparação local). Configurar área de preparação de saudação usando Olá [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet e hello ```-StagingAreaPath``` parâmetro.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

O exemplo hello acima, área de preparação de saudação será definida muito*C:\StagingArea* no objeto do PowerShell Olá ```$setting```. Certifique-se de que Olá a pasta especificada já existe, ou então a confirmação final Olá das configurações de assinatura Olá falhará.

### <a name="encryption-settings"></a>Configurações de criptografia
Olá enviados os dados de backup tooAzure Backup é tooprotect criptografados Olá confidencialidade de dados de saudação. senha de criptografia de saudação é dados de saudação toodecrypt senha"Olá" no tempo de saudação da restauração. É importante tookeep este seguro de informações e seguro depois que ela é definida.

Exemplo hello abaixo, comando primeiro Olá converte a cadeia de caracteres de saudação ```passphrase123456789``` tooa segura cadeia de caracteres e atribui Olá seguro toohello variável string denominada ```$Passphrase```. Olá segundo comando define a cadeia de caracteres segura Olá ```$Passphrase``` como senha Olá para criptografia de backups.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Manter informações de senha Olá seguros e protegidos depois que ela é definida. Você não será capaz de toorestore a dados do Azure sem essa frase secreta.
>
>

Neste ponto, você deveria ter feito todas as toohello de alterações de saudação necessária ```$setting``` objeto. Lembre-se as alterações de saudação do toocommit.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Proteger dados tooAzure Backup
Nesta seção, você adicionará um tooDPM do servidor de produção e, em seguida, proteger o armazenamento do DPM toolocal Olá dados e, em seguida, tooAzure Backup. Exemplos de hello, demonstraremos como tooback backup de arquivos e pastas. Olá lógica pode facilmente ser estendido toobackup qualquer fonte de dados com suporte ao DPM. Todos os backups do DPM são regidos por um GP (Grupo de Proteção) com quatro partes:

1. **Os membros do grupo** é uma lista de todos os objetos protegíveis de saudação (também conhecido como *fontes de dados* no DPM) que você deseja tooprotect em Olá mesmo grupo de proteção. Por exemplo, convém tooprotect produção VMs em um grupo de proteção e bancos de dados do SQL Server em outro grupo de proteção como eles podem ter diferentes requisitos de backup. Antes de fazer backup de qualquer fonte de dados em um servidor de produção, você precisa toomake o hello-se de que o agente do DPM está instalado no servidor de saudação e é gerenciado pelo DPM. Siga as etapas de saudação para [instalando Olá agente do DPM](https://technet.microsoft.com/library/bb870935.aspx) e vinculá-lo toohello apropriado do servidor DPM.
2. **Método de proteção de dados** Especifica os locais de backup Olá destino - fita, disco e nuvem. Em nosso exemplo, protege dados toohello local em disco e toohello na nuvem.
3. Um **agendamento de backup** que especifica quando backups necessário toobe feito e frequência hello dados devem ser sincronizados entre hello servidor DPM e o servidor de produção de hello.
4. Um **agenda de retenção** que especifica quanto tempo os pontos de recuperação de saudação do tooretain no Azure.

### <a name="creating-a-protection-group"></a>Criando um grupo de proteção
Comece criando um novo grupo de proteção usando Olá [DPMProtectionGroup novo](https://technet.microsoft.com/library/hh881722) cmdlet.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Olá acima cmdlet criará um grupo de proteção chamada *ProtectGroup01*. Um grupo de proteção também pode ser modificado posteriormente tooadd toohello backup nuvem do Azure. No entanto, toomake alterações toohello grupo de proteção - novo ou existente - precisamos tooget um identificador em uma *modificável* objeto usando Olá [DPMModifiableProtectionGroup Get](https://technet.microsoft.com/library/hh881713) cmdlet.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Adicionar membros de grupo toohello grupo de proteção
Cada agente do DPM sabe lista Olá de fontes de dados no servidor de saudação que ele está instalado. tooadd toohello uma fonte de dados grupo de proteção, Olá toofirst de necessidades de agente do DPM enviar uma lista de servidor DPM de toohello back Olá fontes de dados. Uma ou mais fontes de dados forem selecionadas e adicionadas toohello grupo de proteção. etapas do PowerShell Olá necessárias tooachieve isso são:

1. Obter uma lista de todos os servidores gerenciados pelo DPM por meio de saudação agente do DPM.
2. Escolher um servidor específico.
3. Obter uma lista de todas as fontes de dados no servidor de saudação.
4. Escolha uma ou mais fontes de dados e adicioná-los toohello grupo de proteção

Olá lista de servidores nos quais Olá agente do DPM está instalado e está sendo gerenciado pelo servidor DPM da saudação é adquirida com hello [DPMProductionServer Get](https://technet.microsoft.com/library/hh881600) cmdlet. Neste exemplo, filtraremos e configuraremos apenas o PS com o nome *productionserver01* para o backup.

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Agora obter lista de saudação de fontes de dados em ```$server``` usando Olá [DPMDatasource Get](https://technet.microsoft.com/library/hh881605) cmdlet. Neste exemplo nós estamos filtrando para volume hello * unidade d:\* que desejamos tooconfigure para backup. Esta fonte de dados é adicionada toohello grupo de proteção usando Olá [DPMChildDatasource adicionar](https://technet.microsoft.com/library/hh881732) cmdlet. Lembre-se de saudação toouse *modificável* objeto do grupo de proteção ```$MPG``` toomake adições de saudação.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Repita essa etapa, quantas vezes forem necessárias, até que você adicionou todos os Olá escolhido o grupo de proteção toohello fontes de dados. Você também pode iniciar com apenas uma fonte de dados e fluxo de trabalho Olá completa para a criação de grupo de proteção de saudação e posteriormente adicionar mais fontes de dados toohello grupo de proteção.

### <a name="selecting-hello-data-protection-method"></a>Selecionar método de proteção de dados hello
Depois de fontes de dados Olá adicionou toohello grupo de proteção, Olá próxima etapa é toospecify o método de proteção de saudação usando Olá [DPMProtectionType conjunto](https://technet.microsoft.com/library/hh881725) cmdlet. Neste exemplo, Olá grupo de proteção está configurado para o disco local e backup na nuvem. Você também precisa toospecify Olá a fonte de dados que você deseja toocloud tooprotect usando Olá [DPMChildDatasource adicionar](https://technet.microsoft.com/library/hh881732.aspx) cmdlet com - sinalizador Online.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Definir o período de retenção de saudação
Definir retenção Olá Olá backup pontos de usando Olá [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet. Enquanto a retenção de saudação ímpar tooset pode parecer antes de agendamento de backup Olá tiver sido definido, usando Olá ```Set-DPMPolicyObjective``` cmdlet automaticamente define uma agenda de backup padrão que pode ser modificada. É sempre agendamento de backup possível tooset Olá primeiro e Olá a política de retenção depois.

O exemplo hello abaixo, Olá define parâmetros de retenção Olá para backups em disco. Isso manterá backups para 10 dias e os dados de sincronização entre servidores de produção de hello e DPM Olá a cada 6 horas. Olá ```SynchronizationFrequencyMinutes``` não define quantas vezes um ponto de backup é criado, mas como dados geralmente são servidor DPM toohello copiado.  Essa configuração impede que os backups fiquem grandes demais.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Intervalos de retenção de saudação para backups vai tooAzure (DPM refere-se toothem como backups Online) podem ser configurados para [usando um esquema de avô-pai-filho (GFS) de retenção de longo prazo](backup-azure-backup-cloud-as-tape.md). Ou seja, você pode definir uma política de retenção combinada que envolva políticas de retenção diárias, semanais, mensais e anuais. Neste exemplo, criamos uma matriz que representa o esquema de retenção complexas Olá que queremos e, em seguida, configurar o período de retenção hello usando Olá [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Agendamento de backup de saudação do conjunto
O DPM define uma agenda de backup padrão automaticamente se você especificar o objetivo de proteção de saudação usando Olá ```Set-DPMPolicyObjective``` cmdlet. os agendamentos padrão Olá toochange, use Olá [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguido por Olá [DPMPolicySchedule conjunto](https://technet.microsoft.com/library/hh881723) cmdlet.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

Em hello, o exemplo acima ```$onlineSch``` é uma matriz que contém a agenda de proteção online existente Olá para Olá grupo de proteção no esquema GFS Olá com quatro elementos:

1. ```$onlineSch[0]```contém a agenda diária Olá
2. ```$onlineSch[1]```contém a agenda semanal Olá
3. ```$onlineSch[2]```contém o agendamento mensal Olá
4. ```$onlineSch[3]```contém a agenda de saudação anual

Portanto, se você precisar agenda semanal do toomodify hello, você precisa toorefer toohello ```$onlineSch[1]```.

### <a name="initial-backup"></a>Backup inicial
Ao fazer backup de uma fonte de dados para Olá primeira vez, o DPM necessidades cria réplica inicial que cria uma cópia completa de saudação toobe de fonte de dados protegido no volume de réplica do DPM. Essa atividade pode ser agendada durante um período específico ou pode ser disparada de manualmente, usando Olá [conjunto DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet com o parâmetro hello ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Alterando o tamanho de saudação de réplica do DPM e o volume de ponto de recuperação
Você também pode alterar o tamanho de saudação do volume de réplica do DPM e a cópia de sombra de volume usando [DPMDatasourceDiskAllocation conjunto](https://technet.microsoft.com/library/hh881618.aspx) cmdlet como no exemplo a seguir de saudação: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manual - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>Confirmar Olá altera toohello grupo de proteção
Finalmente, alterações de saudação precisam toobe confirmada antes do DPM pode fazer backup de saudação por nova configuração de grupo de proteção hello. Isso pode ser feito usando Olá [DPMProtectionGroup conjunto](https://technet.microsoft.com/library/hh881758) cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Exibir pontos de backup Olá
Você pode usar o hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet uma lista de todos os pontos de recuperação para uma fonte de dados. Neste exemplo, iremos:

* busca todas Olá páginas no servidor DPM hello e armazenados em uma matriz```$PG```
* obter Olá fontes de dados correspondente toohello```$PG[0]```
* obter todos os pontos de recuperação Olá para uma fonte de dados.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Restaurar dados protegidos no Azure
A restauração de dados é uma combinação de um objeto ```RecoverableItem``` e um objeto ```RecoveryOption```. Na seção anterior do hello, nós temos uma lista de pontos de backup Olá para uma fonte de dados.

O exemplo hello abaixo, demonstraremos como máquina virtual de toorestore um Hyper-V do Backup do Azure por pontos de backup combinando com hello de destino para recuperação. Este exemplo inclui:

* Criando uma opção de recuperação usando Olá [DPMRecoveryOption novo](https://technet.microsoft.com/library/hh881592) cmdlet.
* Matriz de Olá busca de pontos de backup usando Olá ```Get-DPMRecoveryPoint``` cmdlet.
* Escolhendo um toorestore de ponto de backup do.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

comandos de saudação podem ser facilmente estendidos para qualquer tipo de fonte de dados.

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre o DPM tooAzure Backup consulte [Introdução tooDPM Backup](backup-azure-dpm-introduction.md)
