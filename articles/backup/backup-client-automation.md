---
title: aaaUse PowerShell tooback backup do Windows Server tooAzure | Microsoft Docs
description: Saiba como toodeploy e gerenciar o Backup do Azure usando o PowerShell
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Implantar e gerenciar o backup tooAzure para o cliente do Windows Server/Windows usando o PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Clássico](backup-client-automation-classic.md)
>
>

Este artigo mostra como toouse do PowerShell para configurar o Backup do Azure no Windows Server ou um cliente do Windows e gerenciamento de backup e recuperação.

## <a name="install-azure-powershell"></a>Instalar o Azure Powershell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Este artigo enfoca hello Azure Resource Manager (ARM) e Olá cmdlets do PowerShell de Backup Online da MS que permitem que você toouse um cofre de serviços de recuperação em um grupo de recursos.

Em outubro de 2015, o Azure PowerShell 1.0 foi lançado. Esta versão foi bem-sucedido versão Olá 0.9.8 e colocado sobre alterações significativas, especialmente no padrão de nomenclatura Olá Olá cmdlets. Acompanhamento de cmdlets 1.0 Olá {verbo} padrão de nomenclatura-AzureRm {substantivo;} Por outro lado, não incluem nomes Olá 0.9.8 **Rm** (por exemplo, New-AzureRmResourceGroup em vez de New-AzureResourceGroup). Ao usar o Azure PowerShell 0.9.8, você primeiro deve habilitar o modo de Gerenciador de recursos de Olá executando Olá **Switch-AzureMode AzureResourceManager** comando. Este comando não é necessário na 1.0 ou posterior.

Se quiser toouse seus scripts escritos para o ambiente Olá 0.9.8, Olá 1.0 ou posterior ambiente, você deve atualizar cuidadosamente e testar scripts de saudação em um ambiente de pré-produção antes de usá-las na produção tooavoid impacto inesperado.

[Baixar a versão mais recente de PowerShell Olá](https://github.com/Azure/azure-powershell/releases) (versão mínima necessária é: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
Olá etapas levá-lo na criação de um cofre de serviços de recuperação. Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.

1. Se você estiver usando o Backup do Azure para Olá primeira vez, você deve usar o hello **registro AzureRMResourceProvider** provedor de serviço de recuperação do Azure do cmdlet tooregister Olá com sua assinatura.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Olá Cofre de serviços de recuperação é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos. Você pode usar um grupo de recursos existente ou criar um novo. Ao criar um novo grupo de recursos, especifique o nome de saudação e local para o grupo de recursos de saudação.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. Saudação de uso **AzureRmRecoveryServicesVault novo** novo cofre do cmdlet toocreate hello. Certifique-se de que toospecify Olá mesmo local para o cofre Olá que foi usada para o grupo de recursos de saudação.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
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

Execute o comando hello, **Get-AzureRmRecoveryServicesVault**, e todos os cofres na assinatura de saudação são listados.

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


## <a name="installing-hello-azure-backup-agent"></a>Instalando o agente de Backup do Azure Olá
Antes de instalar o agente de Backup do Azure Olá, você precisará instalador de saudação toohave baixado e presente no saudação do Windows Server. Você pode obter a versão mais recente de saudação do instalador de saudação de saudação [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou da página de painel do Cofre de serviços de recuperação hello. Salvar instalador Olá tooan local facilmente acessível, como * C:\Downloads\*.

Como alternativa, use o downloader de saudação de tooget do PowerShell:
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

Agente de saudação tooinstall, executar Olá seguinte comando em um console do PowerShell com privilégios elevados:

```
PS C:\> MARSAgentInstaller.exe /q
```

Isso instala o agente de saudação com todas as opções padrão de saudação. instalação de saudação leva alguns minutos no plano de fundo de saudação. Se você não especificar Olá */nu* em seguida, Olá **Windows Update** janela será aberta no final de saudação do hello instalação toocheck para todas as atualizações. Uma vez instalado, agente hello serão mostradas na lista Olá de programas instalados.

lista de saudação toosee de instalado programas, consulte muito**painel de controle** > **programas** > **programas e recursos**.

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opções de instalação
toosee todas as opções disponíveis por meio de Olá Olá de linha de comando, use Olá comando a seguir:

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

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>Registro do Windows Server ou Windows client máquina tooa Cofre de serviços de recuperação
Depois que você criar o Cofre de serviços de recuperação de Olá, baixe o agente mais recente hello e as credenciais do cofre hello e armazená-lo em um local conveniente como C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

Saudação do Windows Server ou máquina cliente Windows, executar Olá [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister Olá máquina cofre hello.
Este e outros cmdlets usados para backup, são de um módulo MSONLINE Olá quais Olá Mars AgentInstaller adicionado como parte do processo de instalação de saudação. 

instalador do agente de saudação não atualizar Olá $Env: variável PSModulePath. Isso significa que o carregamento automático do módulo falhará. tooresolve isso você pode fazer a seguir hello:

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

Como alternativa, você pode carregar manualmente Olá módulo em seu script da seguinte maneira:

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

Depois de carregar os cmdlets do Backup Online Olá, é registrar credenciais do cofre hello:


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> Não use o arquivo de credenciais de cofre do caminhos relativos toospecify hello. Você deve fornecer um caminho absoluto como um cmdlet toohello de entrada.
>
>

## <a name="networking-settings"></a>Configurações de rede
Quando a conectividade de saudação do hello Windows máquina toohello que Internet é por meio de um servidor proxy, as configurações de proxy Olá também podem ser fornecidas toohello agente. Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.

Uso de largura de banda também pode ser controlado com opções de saudação do ```work hour bandwidth``` e ```non-work hour bandwidth``` para um determinado conjunto de dias da semana hello.

Configurar detalhes de proxy e de largura de banda de saudação é feita usando Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Configurações de criptografia
Olá enviados os dados de backup tooAzure Backup é tooprotect criptografados Olá confidencialidade de dados de saudação. senha de criptografia de saudação é dados de saudação toodecrypt senha"Olá" no tempo de saudação da restauração.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> Manter informações de senha Olá seguros e protegidos depois que ela é definida. Não será capaz de toorestore a dados do Azure sem essa frase secreta.
>
>

## <a name="back-up-files-and-folders"></a>Fazer backup de arquivos e pastas
Todos os backups de clientes e servidores Windows tooAzure Backup são governados por uma política. política de saudação consiste em três partes:

1. Um **agendamento de backup** que especifica quando backups necessário toobe tomadas e sincronizados com o serviço de saudação.
2. Um **agenda de retenção** que especifica quanto tempo os pontos de recuperação de saudação do tooretain no Azure.
3. Uma **especificação de inclusão/exclusão de arquivo** que determina de que conteúdo deve-se realizar o backup.

Neste documento, já que estamos automatizando o backup, vamos pressupor que nada foi configurado. Começamos criando uma nova política de backup usando Olá [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.

```
PS C:\> $newpolicy = New-OBPolicy
```

Em Olá esse tempo política está vazia e outros cmdlets são necessário toodefine os itens a serem incluídos ou excluídos, quando os backups serão executados e Olá onde os backups serão armazenados.

### <a name="configuring-hello-backup-schedule"></a>Configurar o agendamento de backup Olá
Olá pela primeira vez da saudação 3 partes de uma política é agenda de backup hello, que é criada usando Olá [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet. agendamento de backup Olá define quando backups necessário toobe realizada. Ao criar um agendamento, você precisa toospecify 2 parâmetros de entrada:

* **Dias da semana Olá** backup Olá deve ser executado. Você pode executar o trabalho de backup de saudação em apenas um dia, ou todos os dias da semana hello ou qualquer combinação entre.
* **Horas do dia Olá** quando backup Olá deve ser executado. Você pode definir o too3 diferentes momentos do dia hello quando backup Olá será disparado.

Por exemplo, você poderia configurar uma política de backup que é executada às 16h todo sábado e domingo.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

agendamento de backup Olá precisa toobe associado a uma política e isso pode ser obtido usando Olá [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Configurando uma política de retenção
política de retenção Olá define quanto tempo recuperação pontos criados a partir de trabalhos de backup são mantidos. Ao criar uma nova política de retenção usando Olá [OBRetentionPolicy novo](https://technet.microsoft.com/library/hh770425) cmdlet, você pode especificar Olá de dias que Olá pontos de recuperação de backup é necessário toobe mantida com o Backup do Azure. exemplo Hello abaixo define uma política de retenção de sete dias.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Olá política de retenção deve ser associada com a política principal hello, usando o cmdlet Olá [OBRetentionPolicy conjunto](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>Incluindo e excluindo arquivos toobe backup
Um ```OBFileSpec``` objeto define Olá arquivos toobe incluído e excluído em um backup. Este é um conjunto de regras que verificam a saudação arquivos e pastas protegidos em um computador. Você pode ter muitas regras de inclusão ou exclusão de arquivos conforme necessário e associá-las a uma política. Ao criar um novo objeto OBFileSpec, você pode:

* Especifique a saudação toobe arquivos e pastas incluído
* Especifique a saudação toobe arquivos e pastas excluído
* Especifica recursiva de backup de dados em uma pasta (ou) se apenas Olá nível superior arquivos na pasta especificada Olá devem ser feitos backup.

Olá este último é obtida usando o sinalizador de não - recursivo Olá no comando Olá New-OBFileSpec.

O exemplo hello abaixo, vamos fazer backup de volume c: e d e excluir os binários do sistema operacional Olá na pasta do Windows hello e qualquer pasta temporária. toodo portanto vamos criar duas especificações de arquivo usando Olá [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - uma para inclusão e outra para exclusão. Depois que criar especificações de arquivo hello, eles são associados com a política de saudação usando Olá [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Aplicar a diretiva de saudação
Agora o objeto de diretiva de saudação for concluído e tem um agendamento de backup associado, política de retenção e uma lista de inclusão/exclusão de arquivos. Esta política agora pode ser confirmada para toouse de Backup do Azure. Antes de aplicar Olá recém-criado política Certifique-se de que não há nenhuma política de backup existente associada ao servidor de saudação usando Olá [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet. Remover a política de saudação solicita confirmação. confirmação de saudação tooskip usar Olá ```-Confirm:$false``` sinalizador com hello cmdlet.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Objeto de diretiva de saudação de confirmação é feito usando Olá [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet. Isso também gerará uma solicitação de confirmação. confirmação de saudação tooskip usar Olá ```-Confirm:$false``` sinalizador com hello cmdlet.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

Você pode exibir detalhes de Olá Olá existente da política de backup usando Olá [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet. Você pode detalhamento ainda mais usando Olá [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet para o agendamento de backup hello e hello [OBRetentionPolicy Get](https://technet.microsoft.com/library/hh770427) cmdlet Olá das políticas de retenção

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>Executando um backup ad hoc
Quando uma política de backup foi definida backups Olá ocorrerá por agendamento hello. Também é possível usar Olá acionar um backup ad-hoc [OBBackup início](https://technet.microsoft.com/library/hh770426) cmdlet:

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Restaurar dados por meio do Backup do Azure
Esta seção o guiará pelas etapas de saudação para automatizar a recuperação de dados de Backup do Azure. Fazer assim envolve Olá etapas a seguir:

1. Selecione o volume de origem Olá
2. Escolha um toorestore de ponto de backup
3. Escolha um item toorestore
4. Processo de restauração de saudação do gatilho

### <a name="picking-hello-source-volume"></a>Volume de origem de saudação de separação
Ordem toorestore um item de Backup do Azure, você primeiro precisa tooidentify origem de saudação do item de saudação. Como executamos comandos Olá no contexto de saudação de um servidor do Windows ou um cliente do Windows, a máquina Olá já está identificada. Olá próxima etapa na identificação de fonte de saudação é tooidentify volume de saudação que o contém. Uma lista de volumes ou fontes de backup deste computador pode ser recuperado por meio da execução Olá [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet. Esse comando retorna uma matriz de todas as fontes de saudação backup desse servidor/cliente.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a>Escolhendo um ponto de backup da qual toorestore
Recuperar uma lista de pontos de backup executando Olá [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet com os parâmetros apropriados. Em nosso exemplo, vamos escolher ponto de backup mais recente Olá para o volume de origem Olá *unidade d:* e usá-lo toorecover um arquivo específico.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
objeto Olá ```$rps``` é uma matriz de pontos de backup. Olá primeiro elemento é o último ponto de saudação e enésimo elemento de saudação é ponto mais antigo hello. ponto mais recente do toochoose Olá, vamos usar ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Escolher um item toorestore
Olá tooidentify exato do arquivo ou pasta toorestore, recursivamente usar Olá [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet. Essa hierarquia de pasta maneira Olá possa ser navegada exclusivamente usando Olá ```Get-OBRecoverableItem```.

Neste exemplo, se quisermos que o arquivo de saudação toorestore *finances.xls* podemos fazer referência a esse usando objeto Olá ```$filesFolders[1]```.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

Você também pode procurar itens toorestore usando Olá ```Get-OBRecoverableItem``` cmdlet. Em nosso exemplo, toosearch para *finances.xls* foi possível obter um identificador de arquivo hello executando este comando:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Disparar o processo de restauração Olá
tootrigger o processo de restauração Olá, é preciso primeiro toospecify opções de recuperação de saudação. Isso pode ser feito usando Olá [OBRecoveryOption novo](https://technet.microsoft.com/library/hh770417.aspx) cmdlet. Neste exemplo, vamos supor que queremos arquivos de saudação toorestore muito*C:\temp*. Vamos supor também que desejamos tooskip arquivos já existentes na pasta de destino Olá *C:\temp*. toocreate tal uma opção de recuperação, use Olá comando a seguir:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Agora disparar o processo de restauração hello usando Olá [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando Olá selecionado ```$item``` da saída de saudação de saudação ```Get-OBRecoverableItem``` cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>Desinstalar o agente de Backup do Azure Olá
Desinstalando agente de Backup do Azure Olá pode ser feito usando o comando a seguir de saudação:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Desinstalar os binários de agente de saudação da máquina de saudação tem algumas tooconsider consequências:

* Ele remove o filtro de arquivo hello da máquina de saudação e controle de alterações é interrompido.
* Todas as informações de política são removidas da máquina de hello, mas as informações de política de saudação continuam toobe armazenado no serviço de saudação.
* Todos os agendamentos de backup são removidos e nenhum backup posterior é realizado.

No entanto, Olá dados armazenados no Azure permanece e retidos de acordo com a configuração de política de retenção Olá por você. Os pontos mais antigos são desatualizados automaticamente.

## <a name="remote-management"></a>Gerenciamento remoto
Todo o gerenciamento de saudação em torno de agente de Backup do Azure hello, políticas e fontes de dados pode ser feito remotamente por meio do PowerShell. máquina de saudação que será gerenciada remotamente precisa toobe preparado corretamente.

Por padrão, a saudação serviço WinRM está configurada para inicialização manual. tipo de inicialização de saudação deve ser definido muito*automáticas* e Olá serviço deve ser iniciado. tooverify que Olá serviço WinRM está em execução, o valor Olá Olá propriedade Status deve ser *executando*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

O PowerShell deve ser configurado remotamente.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

máquina Olá agora pode ser gerenciada remotamente - a partir da instalação de saudação do agente de saudação. Por exemplo, hello script a seguir copia o computador remoto do hello agente toohello e instala-o.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o Backup do Azure para Windows Server/Client, consulte

* [Introdução tooAzure Backup](backup-introduction-to-azure-backup.md)
* [Fazer backup de servidores Windows](backup-configure-vault.md)
