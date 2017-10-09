---
title: "aaaConfigure Olá sempre no grupo de disponibilidade em uma VM do Azure usando o PowerShell | Microsoft Docs"
description: "Este tutorial usa recursos que foram criados com o modelo de implantação clássico hello. Use o PowerShell toocreate um grupo de disponibilidade AlwaysOn no Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>Configurar Olá sempre no grupo de disponibilidade em uma VM do Azure com o PowerShell
> [!div class="op_single_selector"]
> * [Clássico: Interface de usuário](../classic/portal-sql-alwayson-availability-groups.md)
> * [Clássico: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Antes de começar, considere que agora você pode concluir esta tarefa no modelo do Azure Resource Manager. O modelo do Azure Resource Manager é recomendável para novas implantações. Confira, [Introdução aos grupos de disponibilidade Always On do SQL Server em máquinas virtuais do Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello.

Máquinas virtuais (VMs) do Azure pode ajudar o custo de saudação de toolower de administradores de banco de dados de um sistema de alta disponibilidade do SQL Server. Este tutorial mostra como tooimplement uma disponibilidade de grupo usando o SQL Server Always On ponta a ponta em um ambiente do Azure. No final de saudação do tutorial hello, sua solução SQL Server Always On no Azure consistirá Olá elementos a seguir:

* Uma rede virtual que contém várias sub-redes, incluindo uma de front-end e uma de back-end.
* Um controlador de domínio com um domínio do Active Directory.
* Duas VMs do SQL Server que são implantados toohello sub-rede de back-end e toohello ingressado no domínio de Active Directory.
* Um cluster de failover do Windows três nós com o modelo de quorum de maioria de nós de saudação.
* Um grupo de disponibilidade com duas réplicas de confirmação síncrona de um banco de dados de disponibilidade.

Esse cenário é uma boa escolha por sua simplicidade no Azure, não pela economia ou outros fatores. Por exemplo, você pode minimizar o número de saudação de VMs para um toosave do grupo de disponibilidade de duas réplicas horas de computação no Azure usando o controlador de domínio hello como testemunha de compartilhamento de arquivo hello quorum em um cluster de failover de dois nós. Esse método reduz a contagem de VM de Olá por um de saudação acima de configuração.

Este tutorial é dirigido a tooshow Olá etapas que são necessária tooset backup Olá descrito solução acima sem elaborar os detalhes de saudação de cada etapa. Portanto, em vez de fornecer as etapas de configuração de saudação GUI, ele usa tootake de scripts do PowerShell você rapidamente a cada etapa. Este tutorial pressupõe o seguinte hello:

* Você já tem uma conta do Azure com assinatura de máquina virtual de saudação.
* Você instalou Olá [cmdlets do PowerShell do Azure](/powershell/azure/overview).
* Você já tem uma compreensão sólida dos grupos de disponibilidade Always On para soluções locais. Para obter mais informações, confira [Grupos de disponibilidade Always On (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Conecte-se tooyour assinatura do Azure e criar rede virtual Olá
1. Em uma janela do PowerShell no computador local, importar Olá módulo do Azure, baixe Olá máquina de tooyour do arquivo de configurações de publicação e conectar-se a sua sessão de PowerShell tooyour assinatura do Azure importando as configurações de publicação Olá baixado.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Olá **AzurePublishSettingsFile Get** comando baixa tooyour máquina e gera um certificado de gerenciamento com o Azure automaticamente. Um navegador é aberto automaticamente e você está tooenter solicitadas Olá credenciais de conta da Microsoft para sua assinatura do Azure. Olá baixado **. publishsettings** arquivo contém todas as informações de saudação necessário toomanage sua assinatura do Azure. Depois de salvar este diretório local do arquivo tooa, importá-lo usando Olá **AzurePublishSettingsFile importação** comando.

   > [!NOTE]
   > arquivo. publishsettings de saudação contém suas credenciais (sem codificação) que são usado tooadminister suas assinaturas do Azure e serviços. prática recomendada de segurança Olá para esse arquivo é toostore-lo temporariamente fora dos diretórios de origem (por exemplo, na pasta de bibliotecas\documentos Olá) e, em seguida, excluí-lo após a importação de saudação. Um usuário mal-intencionado que obtém o arquivo. publishsettings do access toohello pode editar, criar e excluir seus serviços do Azure.

2. Defina uma série de variáveis que você usará toocreate sua nuvem de infraestrutura de TI.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Preste atenção toohello tooensure que os comandos tenham êxito posterior a seguir:

   * Variáveis **$storageAccountName** e **$dcServiceName** devem ser exclusivas porque são usados tooidentify de sua conta de armazenamento de nuvem e o servidor de nuvem, respectivamente, no hello da Internet.
   * Olá nomes que você especificar para variáveis **$affinityGroupName** e **$virtualNetworkName** são configurados no documento de configuração de rede virtual Olá que você usará mais tarde.
   * **$sqlImageName** especifica nome hello atualizado da imagem VM Olá que contém o SQL Server 2012 Service Pack 1 Enterprise Edition.
   * Para simplificar, **Contoso! 000** é Olá a mesma senha que é usada em todo o tutorial todo hello.

3. Crie um grupo de afinidades.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Crie uma rede virtual importando um arquivo de configuração.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    arquivo de configuração de saudação contém Olá documento XML a seguir. Em suma, ele especifica uma rede virtual chamada **ContosoNET** no grupo de afinidade Olá chamado **ContosoAG**. Tem espaço de endereço Olá **10.10.0.0/16** e duas sub-redes, **10.10.1.0/24** e **10.10.2.0/24**, que são sub-rede front hello e posterior, respectivamente. a sub-rede front Olá é onde você pode colocar aplicativos cliente, como o Microsoft SharePoint. subrede back Olá é onde você colocará Olá VMs do SQL Server. Se você alterar Olá **$affinityGroupName** e **$virtualNetworkName** variáveis anteriores, você deve também alterar Olá correspondente nomes abaixo.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Crie uma conta de armazenamento que está associado a grupo de afinidade Olá que você criou e defina-a como conta de armazenamento atual da saudação em sua assinatura.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Crie servidor do controlador de domínio Olá no hello nova nuvem serviço e conjunto de disponibilidade.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Esses comandos conectados Olá coisas a seguir:

   * **New-AzureVMConfig** cria uma configuração de VM.
   * **Adicionar-AzureProvisioningConfig** fornece Olá parâmetros de configuração de um servidor autônomo do Windows.
   * **Adicionar-AzureDataDisk** adiciona Olá disco de dados que você usará para armazenar dados do Active Directory, com hello tooNone de conjunto de opção de cache.
   * **New-AzureVM** cria um novo serviço de nuvem e cria Olá nova VM do Azure no novo serviço de nuvem hello.

7. Espere Olá nova VM toobe totalmente provisionada e baixe a pasta de trabalho de tooyour Olá arquivo de área de trabalho remota. Como hello nova VM do Azure usa um tooprovision muito tempo, Olá `while` loop continua toopoll Olá nova VM até que ele está pronto para uso.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

servidor do controlador de domínio Olá agora está provisionado com êxito. Em seguida, você configurará o domínio do Active Directory Olá neste servidor de controlador de domínio. Janela do PowerShell Olá deixe aberta no computador local. Você vai usá-lo novamente toocreate posterior Olá duas VMs do SQL Server.

## <a name="configure-hello-domain-controller"></a>Configurar o controlador de domínio Olá
1. Conecte-se servidor do controlador de domínio toohello iniciando Olá arquivo da área de trabalho remota. Usar AzureAdmin de nome de usuário e a senha do administrador do computador Olá **Contoso! 000**, que você especificou quando criou Olá nova VM.
2. Abra uma janela do PowerShell no modo de administrador.
3. Execute seguinte Olá **DCPROMO. EXE** tooset do comando backup Olá **corp.contoso.com** domínio, com diretórios de dados de saudação na unidade M.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Após a conclusão do comando hello, Olá VM será reiniciada automaticamente.

4. Conecte novamente o servidor do controlador de domínio toohello iniciando Olá arquivo de área de trabalho remota. Desta vez, faça logon como **CORP\Administrador**.
5. Abra uma janela do PowerShell no modo de administrador e importar o módulo do Active Directory PowerShell hello usando Olá comando a seguir:

        Import-Module ActiveDirectory

6. Execute Olá comandos tooadd três usuários toohello o domínio a seguir.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** é usado tooconfigure tudo relacionado toohello instâncias de serviço do SQL Server, o cluster de failover hello e o grupo de disponibilidade de saudação. **CORP\SQLSvc1** e **CORP\SQLSvc2** são usados como contas de serviço do SQL Server Olá Olá duas VMs do SQL Server.
7. A seguir Olá Avançar, execute comandos toogive **CORP\Install** Olá objetos de computador toocreate permissões no domínio hello.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Olá GUID especificado acima é hello GUID para o tipo de objeto de computador hello. Olá **CORP\Install** conta precisa Olá **ler todas as propriedades** e **criar objetos de computador** Olá de toocreate permissão Active Direct objetos para o failover de saudação cluster. Olá **ler todas as propriedades** permissão já foi atribuída tooCORP\Install por padrão, portanto, você não precisa toogrant-lo explicitamente. Para obter mais informações sobre as permissões que são necessárias cluster de failover do toocreate hello, consulte [guia do passo a passo de Cluster de Failover: Configurando contas no Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Agora que você terminou a configuração do Active Directory e objetos de saudação do usuário, você criará duas VMs do SQL Server e associá-las toothis domínio.

## <a name="create-hello-sql-server-vms"></a>Criar hello VMs do SQL Server
1. Continue toouse Olá PowerShell janela aberta no computador local. Defina Olá variáveis adicionais a seguir:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    Olá endereço IP **10.10.0.4** normalmente é atribuído toohello primeira máquina virtual que você cria no hello **10.10.0.0/16** sub-rede da rede virtual do Azure. Você deve verificar se este é o endereço de saudação do seu servidor do controlador de domínio executando **IPCONFIG**.
2. Execução Olá Olá de toocreate comandos conectados a seguir primeiro VM no cluster de failover hello, denominado **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Observe o seguinte de saudação sobre Olá comando acima:

   * **New-AzureVMConfig** cria uma configuração de VM com o nome do conjunto de disponibilidade desejado hello. Olá VMs subsequentes serão criadas com hello mesmo nome do conjunto de disponibilidade para que elas são unidas toohello mesmo conjunto de disponibilidade.
   * **Adicionar-AzureProvisioningConfig** junções Olá domínio do Active Directory do VM toohello que você criou.
   * **Conjunto AzureSubnet** casas Olá VM na sub-rede back hello.
   * **New-AzureVM** cria um novo serviço de nuvem e cria Olá nova VM do Azure no novo serviço de nuvem hello. Olá **DnsSettings** parâmetro especifica o servidor DNS Olá para servidores no novo serviço de nuvem Olá Olá tem endereço IP hello **10.10.0.4**. Esse é o endereço IP de saudação do servidor de saudação do controlador de domínio. Esse parâmetro é necessário tooenable Olá novas VMs no domínio do Active Directory do hello nuvem serviço toojoin toohello com êxito. Sem esse parâmetro, você deve manualmente definir configurações de IPv4 Olá em seu servidor de controlador de domínio do VM toouse hello como servidor DNS primário Olá após Olá VM é provisionada e, em seguida, ingressar em domínio do Active Directory do hello VM toohello.
3. Saudação de execução a seguir canalizado comandos toocreate Olá VMs do SQL Server, chamado **ContosoSQL1** e **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Observe o seguinte de saudação sobre Olá comandos acima:

   * **New-AzureVMConfig** usa Olá mesmo nome do conjunto de disponibilidade como servidor de controlador de domínio hello e usa Olá imagem do SQL Server 2012 Service Pack 1 Enterprise Edition na Galeria de máquinas virtuais de saudação. Ele também define Olá operacional sistema tooread do cache de disco somente (sem cache de gravação). É recomendável que você migre Olá banco de dados arquivos tooa disco de dados separado anexar toohello VM e configurá-lo com nenhuma leitura ou gravação em cache. No entanto, Olá próxima melhor é tooremove cache de gravação no disco do sistema operacional Olá porque você não pode remover cache de leitura no disco do sistema operacional hello.
   * **Adicionar-AzureProvisioningConfig** junções Olá domínio do Active Directory do VM toohello que você criou.
   * **Conjunto AzureSubnet** casas Olá VM na sub-rede back hello.
   * **Adicionar-AzureEndpoint** adiciona pontos de extremidade de acesso para que os aplicativos cliente possam acessar essas instâncias de serviços do SQL Server no hello da Internet. Portas diferentes são atribuídas tooContosoSQL1 e ContosoSQL2.
   * **New-AzureVM** cria Olá nova VM do SQL Server no hello mesmo serviço de nuvem como ContosoQuorum. Você deve colocar Olá VMs no hello mesmo serviço de nuvem se você deseja que eles toobe em Olá mesmo conjunto de disponibilidade.
4. Aguarde para cada toobe VM totalmente provisionado e toodownload cada VM seu diretório de trabalho de tooyour de arquivo de área de trabalho remota. Olá `for` loop for percorre Olá três novas VMs e executa comandos de saudação dentro Olá chaves de nível superior para cada um deles.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    Olá VMs do SQL Server agora estão provisionadas e em execução, mas ele estão instalado com o SQL Server com as opções padrão.

## <a name="initialize-hello-failover-cluster-vms"></a>Inicializar máquinas virtuais do cluster de failover Olá
Nesta seção, você precisa toomodify Olá três servidores que você usará no cluster de failover do hello e instalação do SQL Server hello. Especificamente:

* Todos os servidores: você precisa Olá tooinstall **Clustering de Failover** recurso.
* Todos os servidores: É necessário tooadd **CORP\Install** como máquina Olá **administrador**.
* ContosoSQL1 e ContosoSQL2 somente: É necessário tooadd **CORP\Install** como um **sysadmin** função no banco de dados de padrão de saudação.
* ContosoSQL1 e ContosoSQL2 somente: É necessário tooadd **NT AUTHORITY\System** como uma entrada com hello as seguintes permissões:

  * Alterar qualquer grupo de disponibilidade
  * Conectar o SQL
  * Exibir o estado do servidor
* ContosoSQL1 e ContosoSQL2 somente: Olá **TCP** protocolo já está habilitado em Olá VM do SQL Server. No entanto, você ainda precisa firewall de saudação tooopen para acesso remoto do SQL Server.

Agora, você está pronto toostart. Começando com **ContosoQuorum**, siga as etapas de saudação abaixo:

1. Conecte-se muito**ContosoQuorum** iniciando Olá arquivos de área de trabalho remota. Usar nome de usuário do administrador do computador Olá **AzureAdmin** e a senha **Contoso! 000**, que você especificou quando criou Olá VMs.
2. Verifique se que os computadores Olá tem Unidos com êxito muito**corp.contoso.com**.
3. Aguarde toofinish de instalação do SQL Server Olá Olá automatizada tarefas de inicialização antes de continuar em execução.
4. Abra uma janela do PowerShell no modo de administrador.
5. Instale o recurso de cluster de Failover do Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Adicione **CORP\Install** como um administrador local.

        net localgroup administrators "CORP\Install" /Add
7. Saia de ContosoQuorum. A tarefa nesse servidor foi concluída.

        logoff.exe

Em seguida, inicialize **ContosoSQL1** e **ContosoSQL2**. Siga as etapas de saudação abaixo, que são idênticas para ambas as VMs do SQL Server.

1. Conecte toohello duas VMs do SQL Server, iniciando Olá arquivos da área de trabalho remota. Usar nome de usuário do administrador do computador Olá **AzureAdmin** e a senha **Contoso! 000**, que você especificou quando criou Olá VMs.
2. Verifique se que os computadores Olá tem Unidos com êxito muito**corp.contoso.com**.
3. Aguarde toofinish de instalação do SQL Server Olá Olá automatizada tarefas de inicialização antes de continuar em execução.
4. Abra uma janela do PowerShell no modo de administrador.
5. Instale o recurso de cluster de Failover do Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Adicione **CORP\Install** como um administrador local.

        net localgroup administrators "CORP\Install" /Add
7. Importe Olá provedor SQL Server PowerShell.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Adicionar **CORP\Install** como uma função de sysadmin Olá Olá padrão instância do SQL Server.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Adicionar **NT AUTHORITY\System** como uma entrada com permissões de saudação três descrito acima.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. Abra o firewall Olá para acesso remoto do SQL Server.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Saia de ambas as VMs.

         logoff.exe

Por fim, você está pronto tooconfigure grupo de disponibilidade de saudação. Você usará tooperform do provedor do SQL Server PowerShell Olá todos Olá funcionam em **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Configurar o grupo de disponibilidade Olá
1. Conecte-se muito**ContosoSQL1** novamente por iniciando Olá arquivos da área de trabalho remota. Em vez de entrar usando a conta da máquina hello, entrar usando **CORP\Install**.
2. Abra uma janela do PowerShell no modo de administrador.
3. Defina Olá variáveis a seguir:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Importe Olá provedor SQL Server PowerShell.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Alterar a conta de serviço do SQL Server Olá para ContosoSQL1 tooCORP\SQLSvc1.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Alterar a conta de serviço do SQL Server Olá para ContosoSQL2 tooCORP\SQLSvc2.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Baixar **CreateAzureFailoverCluster.ps1** de [criar o Cluster de Failover para grupos de disponibilidade AlwaysOn em VM do Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello diretório de trabalho local. Você usará essa toohelp de script que você criar um cluster de failover funcional. Para obter informações importantes sobre como o Clustering de Failover do Windows interage com hello Azure de rede, consulte [alta disponibilidade e recuperação de desastres para o SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Alterar o diretório de trabalho tooyour e criar o cluster de failover de saudação com script hello baixado.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Habilitar grupos de disponibilidade AlwaysOn para instâncias de SQL Server saudação padrão em **ContosoSQL1** e **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Crie um diretório de backup e conceda permissões para contas de serviço do SQL Server hello. Você usará esse banco de dados do diretório tooprepare Olá disponibilidade na réplica secundária hello.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Criar um banco de dados em **ContosoSQL1** chamado **MyDB1**, faça um backup completo e um backup de log e restaure-os em **ContosoSQL2** com hello **WITH NORECOVERY** opção.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Criar pontos de extremidade de grupo de disponibilidade Olá em Olá VMs do SQL Server e defina as permissões adequadas Olá nos pontos de extremidade de saudação.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Crie hello réplicas de disponibilidade.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Finalmente, crie o grupo de disponibilidade hello e o grupo de disponibilidade de toohello do junção Olá réplica secundária.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Próximas etapas
Agora você implementou com êxito o SQL Server Always On criando um grupo de disponibilidade no Azure. tooconfigure um ouvinte para esse grupo de disponibilidade, consulte [configurar um ouvinte de ILB para grupos de disponibilidade AlwaysOn no Azure](../classic/ps-sql-int-listener.md).

Para obter outras informações sobre como usar o SQL Server no Azure, veja [SQL Server nas Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
