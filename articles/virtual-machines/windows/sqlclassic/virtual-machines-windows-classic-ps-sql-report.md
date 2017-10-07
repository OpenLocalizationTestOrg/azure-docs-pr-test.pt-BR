---
title: "aaaUse PowerShell tooCreate uma VM com um modo de servidor de relatório nativo | Microsoft Docs"
description: "Este tópico descreve e orienta você durante implantação hello e a configuração de um servidor de relatório de modo nativo do SQL Server Reporting Services em uma máquina Virtual do Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Use o PowerShell tooCreate um Azure VM com um modo de servidor de relatório nativo
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Este tópico descreve e orienta você durante implantação hello e a configuração de um servidor de relatório de modo nativo do SQL Server Reporting Services em uma máquina Virtual do Azure. Olá etapas neste documento, use uma combinação de etapas manuais toocreate Olá VM e um script do Windows PowerShell tooconfigure Reporting Services em Olá VM. script de configuração de saudação inclui a abertura de uma porta de firewall para HTTP ou HTTPs.

> [!NOTE]
> Se você não precisa **HTTPS** no servidor de relatório hello, **pular a etapa 2**.
> 
> Depois de criar hello VM na etapa 1, acesse servidor de relatório toohello seção Use script tooconfigure hello e HTTP. Depois de executar o script hello, o servidor de relatório de saudação é toouse pronto.

## <a name="prerequisites-and-assumptions"></a>Pré-requisitos e suposições
* **Assinatura do Azure**: Verifique se o número de saudação de núcleos disponíveis em sua assinatura do Azure. Se você criar hello recomendado tamanho da VM do **A3**, você precisa **4** núcleos disponíveis. Se você usar um tamanho de VM **A2**, precisará de **2** núcleos disponíveis.
  
  * limite de núcleo de saudação tooverify de sua assinatura, Olá portal clássico do Azure, clique em configurações no painel esquerdo do hello e, em seguida, clique em uso no menu superior hello.
  * cota de núcleo Olá tooincrease, entre em contato com [suporte do Azure](https://azure.microsoft.com/support/options/). Para saber mais sobre o tamanho da VM, consulte [Tamanhos de máquinas virtuais do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Scripts do Windows PowerShell**: tópico Olá pressupõe que você tenha um conhecimento prático básico do Windows PowerShell. Para obter mais informações sobre como usar o Windows PowerShell, consulte o seguinte hello:
  
  * [Iniciando o Windows PowerShell no Windows Server](https://technet.microsoft.com/library/hh847814.aspx)
  * [Introdução ao Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>Etapa 1: provisionar uma máquina virtual do Azure
1. Procure toohello portal clássico do Azure.
2. Clique em **máquinas virtuais** no painel esquerdo da saudação.
   
    ![máquinas virtuais do microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. Clique em **Novo**.
   
    ![botão novo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Clique em **Da Galeria**.
   
    ![nova vm da galeria](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Clique em **SQL Server 2014 RTM Standard – Windows Server 2012 R2** e, em seguida, clique em Olá seta toocontinue.
   
    ![Próximo](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Se precisar de dados do Reporting Services Olá controlados por recursos de assinaturas, escolha **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**. Para obter mais informações sobre o suporte de recursos e edições do SQL Server, consulte [recursos com suporte Olá edições do SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. Em Olá **configuração de máquina Virtual** página, edite Olá campos a seguir:
   
   * Se houver mais de um **data de lançamento de versão**, selecione Olá a versão mais recente.
   * **Nome da máquina virtual**: nome da máquina Olá também é usado na próxima página de configuração hello como nome de DNS do serviço de nuvem saudação padrão. nome DNS Olá deve ser exclusivo entre saudação do serviço do Azure. Considere configurar Olá VM com um nome de computador que descreve quais Olá VM é usada para. Por exemplo, ssrsnativecloud.
   * **Camada**: Standard
   * **Tamanho: A3** Olá recomenda tamanho da VM para cargas de trabalho do SQL Server. Se uma VM é usada apenas como um servidor de relatório, um tamanho VM de A2 será suficiente a menos que o servidor de relatório Olá experimente uma grande carga de trabalho. Para saber mais sobre preços da VM, consulte [Preços das Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Novo nome de usuário**: nome de saudação fornecido é criado como um administrador no hello VM.
   * **Nova Senha** e **Confirmar**. Essa senha é usada para a nova conta de administrador hello e é recomendável que usar uma senha forte.
   * Clique em **Avançar**. ![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. Na página seguinte do hello, edite Olá campos a seguir:
   
   * **Serviço de Nuvem**: selecione **Criar um novo Serviço de Nuvem**.
   * **Nome DNS do serviço de nuvem**: Este é o nome DNS público de saudação do hello serviço de nuvem que está associado a saudação VM. saudação padrão é Olá nome digitado no nome da VM hello. Se em etapas posteriores do tópico hello, você cria um certificado SSL confiável e, em seguida, o nome DNS de saudação é usado para valor Olá Olá "**emitido para**" do certificado de saudação.
   * **Afinidade de região/grupo/Rede Virtual**: escolha Olá região mais próxima tooyour os usuários finais.
   * **Conta de Armazenamento**: use uma conta de armazenamento gerada automaticamente.
   * **Conjunto de Disponibilidades**: nenhum.
   * **Pontos de EXTREMIDADE** manter Olá **área de trabalho remota** e **PowerShell** pontos de extremidade e, em seguida, adicione o ponto de extremidade HTTP ou HTTPS, dependendo do seu ambiente.
     
     * **HTTP**: Olá padrão portas públicas e privadas são **80**. Observe que se você usar uma porta privada diferente de 80, modifique **$HTTPport = 80** no script de http hello.
     * **HTTPS**: Olá padrão portas públicas e privadas são **443**. Uma prática recomendada de segurança é a porta privada do toochange hello e configurar seu firewall e hello relatório toouse Olá privada porta do servidor. Para obter mais informações sobre pontos de extremidade, consulte [como tooSet a comunicação com uma máquina Virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Observe que se você usar uma porta diferente de 443, altere o parâmetro hello **$HTTPsport = 443** em Olá script HTTPS.
   * Clique em Próximo. ![Próximo](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. Na última página do Assistente de Olá Olá, mantenha o padrão de saudação **instalar agente de VM de saudação** selecionado. Olá etapas neste tópico não utilizam o agente de VM hello, mas se você planejar tookeep essa VM, extensões e agente VM Olá permitirá que você tooenhance he CM.  Para obter mais informações sobre o agente de VM hello, consulte [agente de VM e extensões – parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). Uma saudação extensões padrão instaladas em execução é extensão "BGINFO" hello exibidas na área de trabalho VM hello, informações do sistema, como IP interno e sem espaço em disco.
9. Clique em Concluído. ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Olá **Status** de saudação VM exibe como **iniciando (Provisionando)** durante o processo de provisionamento de saudação e, em seguida, é exibido como **executando** quando Olá VM é provisionada e pronta toouse.

## <a name="step-2-create-a-server-certificate"></a>Etapa 2: criar um certificado de servidor
> [!NOTE]
> Se você não exigir HTTPS no servidor de relatório hello, você pode **pular a etapa 2** e vá seção toohello **usar HTTP e o servidor de relatório de saudação do script tooconfigure**. Use Olá HTTP script tooquickly configurar servidor de relatório hello e relatório Olá servidor será toouse pronto.

Na ordem toouse HTTPS na VM de Olá, é necessário um certificado SSL confiável. Dependendo do cenário, você pode usar uma saudação dois métodos a seguir:

* Um certificado SSL válido emitido por uma Autoridade de Certificação (CA) e de confiança da Microsoft. certificados de raiz da autoridade de certificação Olá são necessário toobe distribuído por meio de saudação Microsoft Root Certificate Program. Para obter mais informações sobre este programa, consulte [Windows e Windows Phone 8 SSL Root Certificate Program (membros CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) e [toohello de Introdução do Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Um certificado autoassinado. Os certificados autoassinados não são recomendados para ambientes de produção.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse um certificado criado por uma autoridade de certificação confiável (CA)
1. **Solicitar um certificado de servidor para o site de saudação de uma autoridade de certificação**. 
   
    Você pode usar o hello Assistente de certificado de servidor Web ou toogenerate um arquivo de solicitação de certificado (Certreq.txt) que você enviar tooa autoridade de certificação ou toogenerate uma solicitação para uma autoridade de certificação online. Por exemplo, os Serviços de Certificados da Microsoft no Windows Server 2012. Dependendo do nível de saudação de garantia de identificação fornecida pelo certificado de servidor, é dias tooseveral meses para tooapprove de autoridade de certificação Olá sua solicitação e envie um arquivo de certificado. 
   
    Para obter mais informações sobre como solicitar certificados de servidor, consulte o seguinte hello: 
   
   * Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).
   * TooAdminister de ferramentas de segurança do Windows Server 2012.
     
     [TooAdminister de ferramentas de segurança do Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Olá **emitido para** campo de saudação confiável certificado SSL deve ser Olá mesmo como Olá **nome de DNS do serviço de nuvem** você usou para Olá nova VM.

2. **Instalar o certificado de servidor de saudação no servidor de Web hello**. Nesse caso, o servidor de Web Hello é Olá VM que hospeda Olá servidor de relatório e site Olá é criado em etapas posteriores quando você configurar o Reporting Services. Para obter mais informações sobre como instalar o certificado do servidor de saudação no servidor de Web hello usando o snap-in do MMC do certificado hello, consulte [instalar um certificado de servidor](https://technet.microsoft.com/library/cc740068).
   
    Se você quiser que o script de saudação toouse incluído neste tópico, o servidor de relatório Olá tooconfigure, Olá valor de certificados Olá **impressão digital** é exigido como um parâmetro de script hello. Consulte Olá próxima seção para obter detalhes sobre como tooobtain Olá a impressão digital do certificado de saudação.
3. Atribua o servidor de relatório toohello do certificado de servidor hello. atribuição de saudação é concluída na próxima seção, hello quando você configura o servidor de relatório hello.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>Olá toouse certificado autoassinado de máquinas virtuais
Um certificado autoassinado foi criado no hello VM quando Olá VM foi provisionada. certificado de saudação tem Olá mesmo nome como Olá nome DNS da VM. Erros de certificado tooavoid ordem, é necessário certificado Olá é confiável no hello própria VM e também por todos os usuários do site de saudação.

1. tootrust Olá autoridade de certificação raiz do certificado Olá Olá VM Local, adicione Olá certificado toohello **autoridades de certificação raiz confiáveis**. seguir Olá é um resumo das etapas de saudação necessárias. Para obter etapas detalhadas sobre como tootrust Olá autoridade de certificação, consulte [instalar um certificado de servidor](https://technet.microsoft.com/library/cc740068).
   
   1. Olá portal clássico do Azure, selecione Olá VM e clique em conectar. Dependendo da configuração do navegador, talvez seja solicitado toosave um arquivo. rdp para conexão toohello VM.
      
       ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Use o nome da VM Olá usuário, nome de usuário e senha configurados quando você criou Olá VM. 
      
       Por exemplo, Olá a imagem a seguir, Olá VM nome é **ssrsnativecloud** e nome de usuário Olá **testuser**.
      
       ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Execute mmc.exe. Para obter mais informações, consulte [como: exibir certificados com hello Snap-in do MMC](https://msdn.microsoft.com/library/ms788967.aspx).
   3. No aplicativo de console hello **arquivo** menu Adicionar Olá **certificados** snap-in, selecione **conta de computador** quando solicitado e, em seguida, clique em **Avançar**.
   4. Selecione **computador Local** toomanage e, em seguida, clique em **concluir**.
   5. Clique em **Okey** e, em seguida, expanda Olá **certificados - Personal** nós e clique **certificados**. Olá certificado é nomeado após o nome DNS de saudação do hello VM e termina com **cloudapp.net**. Nome do certificado Olá de mouse e clique em **cópia**.
   6. Expanda Olá **autoridades de certificação raiz confiáveis** nó e, em seguida, clique com botão direito **certificados** e, em seguida, clique em **colar**.
   7. toovalidate, duplo clique no nome do certificado de saudação em **autoridades de certificação raiz confiáveis** e verifique se não existem erros e veja seu certificado. Se você quiser toouse Olá HTTPS script incluído neste tópico, o servidor de relatório do tooconfigure hello, Olá valor de certificados Olá **impressão digital** é exigido como um parâmetro de script hello. **valor de impressão digital Olá tooget**, conclua Olá seguinte. Há também uma impressão digital saudação do PowerShell exemplo tooretrieve na seção [usar HTTPS e servidor de relatório do script tooconfigure Olá](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Clique duas vezes no nome de saudação do certificado de hello, por exemplo ssrsnativecloud.cloudapp.net.
      2. Clique em Olá **detalhes** guia.
      3. Clique em **Impressão digital**. valor de saudação da impressão digital de saudação é exibido no campo de detalhes hello, por exemplo, a6 08 3C df f9 0b f7 e3 7c 25 ed a4 ed 7e CA 91 9C 2C fb 2f.
      4. Copie a impressão digital de saudação e salvar o valor de saudação para mais tarde ou edite o script hello agora.
      5. (*) Antes de executar o script hello, remova os espaços de saudação entre Olá pares de valores. Por exemplo impressão digital de saudação observada anteriormente agora seria a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.
      6. Atribua o servidor de relatório toohello do certificado de servidor hello. atribuição de saudação é concluída na próxima seção, hello quando você configura o servidor de relatório hello.

Se você estiver usando um certificado SSL autoassinado, o nome de Olá no certificado Olá corresponde já Olá hostname de saudação VM. Portanto, Olá DNS da máquina Olá já estará registrado globalmente e pode ser acessado de qualquer cliente.

## <a name="step-3-configure-hello-report-server"></a>Etapa 3: Configurar Olá servidor de relatório
Esta seção explica como configurar Olá VM como um servidor de relatório de modo nativo do Reporting Services. Você pode usar um Olá servidor de relatório de saudação de tooconfigure métodos a seguir:

* Usar o servidor de relatório do hello script tooconfigure Olá
* Olá tooConfigure Use o Gerenciador de configuração do servidor de relatório.

Para obter etapas mais detalhadas, consulte a seção de saudação [toohello conectar máquina Virtual e iniciar Olá Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Observação de autenticação:** a autenticação do Windows é hello método de autenticação recomendado e é autenticação do saudação padrão do Reporting Services. Somente os usuários que estão configurados em Olá VM podem acessar o Reporting Services e atribuído tooReporting funções dos serviços.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Usar servidor de relatório do script tooconfigure hello e HTTP
toouse saudação do Windows PowerShell script tooconfigure Olá servidor de relatório, Olá concluir as etapas a seguir. configuração de saudação inclui HTTP, HTTPS não:

1. Olá portal clássico do Azure, selecione Olá VM e clique em conectar. Dependendo da configuração do navegador, talvez seja solicitado toosave um arquivo. rdp para conexão toohello VM.
   
    ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Use o nome da VM Olá usuário, nome de usuário e senha configurados quando você criou Olá VM. 
   
    Por exemplo, Olá a imagem a seguir, Olá VM nome é **ssrsnativecloud** e nome de usuário Olá **testuser**.
   
    ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. No hello VM, abra **o Windows PowerShell ISE** com privilégios administrativos. Olá PowerShell ISE é instalado por padrão no Windows server 2012. É recomendável que usar Olá ISE em vez de uma janela padrão do Windows PowerShell para que colar o script hello em Olá ISE, modificar o script hello e, em seguida, execute o script hello.
3. No ISE do Windows PowerShell, clique em Olá **exibição** menu e clique **Mostrar painel de Script**.
4. Copiar Olá script a seguir e, em seguida, cole o script hello no painel de script do Windows PowerShell ISE hello.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Se você criou Olá VM com uma porta HTTP diferente de 80, modifique o parâmetro hello $HTTPport = 80.
6. script Hello está configurado atualmente para o Reporting Services. Se você quiser toorun script de saudação do Reporting Services, modificar a parte de saudação caminho toohello namespace versão Olá muito "v11" na instrução Olá Get-WmiObject.
7. Execute o script hello.

**Validação**: tooverify funcionalidade de servidor de relatório básico hello está funcionando, consulte Olá [Verificar configuração de saudação](#verify-the-configuration) seção mais adiante neste tópico.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Usar o servidor de relatório do script tooconfigure hello e HTTPS
toouse do Windows PowerShell tooconfigure Olá servidor de relatório, Olá concluir as etapas a seguir. configuração de saudação inclui HTTPS, não HTTP.

1. Olá portal clássico do Azure, selecione Olá VM e clique em conectar. Dependendo da configuração do navegador, talvez seja solicitado toosave um arquivo. rdp para conexão toohello VM.
   
    ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Use o nome da VM Olá usuário, nome de usuário e senha configurados quando você criou Olá VM. 
   
    Por exemplo, Olá a imagem a seguir, Olá VM nome é **ssrsnativecloud** e nome de usuário Olá **testuser**.
   
    ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. No hello VM, abra **o Windows PowerShell ISE** com privilégios administrativos. Olá PowerShell ISE é instalado por padrão no Windows server 2012. É recomendável que usar Olá ISE em vez de uma janela padrão do Windows PowerShell para que colar o script hello em Olá ISE, modificar o script hello e, em seguida, execute o script hello.
3. tooenable a execução de scripts, executados Olá comando do Windows PowerShell a seguir:
   
        Set-ExecutionPolicy RemoteSigned
   
    Você pode executar Olá política de saudação tooverify a seguir:
   
        Get-ExecutionPolicy
4. Em **o Windows PowerShell ISE**, clique em Olá **exibição** menu e clique **Mostrar painel de Script**.
5. Copie Olá seguinte script e cole-o no painel de script do Windows PowerShell ISE hello.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Modificar Olá **$certificatehash** parâmetro no script hello:
   
   * Esse é um parâmetro **obrigatório** . Se você não salvar o valor de saudação do certificado de etapas anteriores Olá, use um dos Olá após o valor de hash de certificado do métodos toocopy Olá da impressão digital de certificados hello.:
     
       No hello VM, abra o Windows PowerShell ISE e execute Olá comando a seguir:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       saída de Hello procurará a seguir toohello semelhante. Se o script hello retorna uma linha em branco, Olá VM não tem um certificado configurado por exemplo, consulte a seção Olá [toouse Olá certificado autoassinado de máquinas virtuais](#to-use-the-virtual-machines-self-signed-certificate).
     
     OU
   * Em Olá VM executar mmc.exe e adicione Olá **certificados** snap-in.
   * Em Olá **autoridades de certificação raiz confiáveis** nó clique duas vezes em seu nome de certificado. Se você estiver usando um certificado autoassinado de saudação do hello VM, o certificado de saudação é nomeado após o nome DNS de saudação do hello VM e termina com **cloudapp.net**.
   * Clique em Olá **detalhes** guia.
   * Clique em **Impressão digital**. valor de saudação da impressão digital de saudação é exibido no campo de detalhes hello, por exemplo af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 4f 66 c3 31 90 48
   * **Antes de executar o script hello**, remova os espaços de saudação entre Olá pares de valores. Por exemplo, af1160b64b288d890a8212ff6ba9c3664f319048
7. Modificar Olá **$httpsport** parâmetro: 
   
   * Se você usou a porta 443 para o ponto de extremidade HTTPS hello, em seguida, você não é necessário tooupdate esse parâmetro no script hello. Caso contrário, use o valor da porta Olá selecionado quando você configurou o ponto de extremidade privado de HTTPS de saudação em Olá VM.
8. Modificar Olá **$DNSName** parâmetro: 
   
   * Olá script está configurado para um certificado curinga $DNSName = "+". Se você não fizer nenhuma tooconfigure desejados para uma associação de certificado curinga, comente $DNSName = "+"e habilitar Olá após a linha, referência de $DNSNAme completo hello, $DNSName="$server.cloudapp.net # #".
     
       Altere o valor de saudação $DNSName se você não quiser que o nome DNS de toouse Olá máquina virtual do Reporting Services. Se você usar o parâmetro hello, certificado Olá também deve usar esse nome e registrar Olá nome globalmente em um servidor DNS.
9. script Hello está configurado atualmente para o Reporting Services. Se você quiser toorun script de saudação do Reporting Services, modificar a parte de saudação caminho toohello namespace versão Olá muito "v11" na instrução Olá Get-WmiObject.
10. Execute o script hello.

**Validação**: tooverify funcionalidade de servidor de relatório básico hello está funcionando, consulte Olá [Verificar configuração de saudação](#verify-the-connection) seção mais adiante neste tópico. associação de certificado Olá tooverify abra um prompt de comando com privilégios administrativos e execute Olá comando a seguir:

    netsh http show sslcert

resultado de saudação incluirá o seguinte hello:

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Olá tooConfigure Use o Gerenciador de configuração do servidor de relatório
Se você não quiser que servidor de relatório toorun Olá PowerShell script tooconfigure hello, siga as etapas de saudação essa seção toouse Olá Reporting Services modo nativo configuration manager tooconfigure Olá servidor de relatório.

1. Olá portal clássico do Azure, selecione Olá VM e clique em conectar. Use o nome de usuário hello e senha configurados quando você criou Olá VM.
   
    ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Execute o Windows update e instalar atualizações toohello VM. Se for necessária uma reinicialização de saudação VM, reiniciar Olá VM e reconecte toohello VM de saudação portal clássico do Azure.
3. Saudação do menu de início em Olá VM, digite **Reporting Services** e abra **Reporting Services Configuration Manager**.
4. Deixe valores padrão de saudação para **nome do servidor** e **instância de servidor de relatório**. Clique em **Conectar**.
5. No painel esquerdo do hello, clique em **URL do serviço Web**.
6. Por padrão, o RS está configurado para a porta HTTP 80 com IP "Todos Atribuídos". tooadd HTTPS:
   
   1. Em **certificado SSL**: Olá selecione certificado toouse, por exemplo, [nome da VM]. cloudapp.net. Se nenhum certificado estiver listado, consulte a seção de saudação **etapa 2: criar um certificado de servidor** para obter informações sobre como tooinstall e confiança Olá certificado Olá VM.
   2. Em **Porta SSL**: escolha 443. Se você configurou o ponto de extremidade privado de HTTPS de saudação em Olá VM com uma porta particular diferente, use esse valor aqui.
   3. Clique em **aplicar** e aguarde Olá operação toocomplete.
7. No painel esquerdo do hello, clique em **banco de dados**.
   
   1. Clique em **Alterar Banco de Dado**s.
   2. Clique em **Criar um novo banco de dados do servidor de relatório** e clique em **Próximo**.
   3. Deixe o padrão de saudação **nome do servidor**: Nomeie Olá VM e deixe o padrão de saudação **tipo de autenticação** como **usuário atual** – **asegurançaintegrada**. Clique em **Avançar**.
   4. Deixe o padrão de saudação **nome do banco de dados** como **ReportServer** e clique em **próximo**.
   5. Deixe o padrão de saudação **tipo de autenticação** como **credenciais de serviço** e clique em **próximo**.
   6. Clique em **próximo** em Olá **resumo** página.
   7. Quando a configuração de saudação estiver concluída, clique em **concluir**.
8. No painel esquerdo do hello, clique em **URL do Report Manager**. Deixe o padrão de saudação **Diretório Virtual** como **relatórios** e clique em **aplicar**.
9. Clique em **Exit** tooclose Olá Reporting Services Configuration Manager.

## <a name="step-4-open-windows-firewall-port"></a>Etapa 4: abrir a porta do Firewall do Windows
> [!NOTE]
> Se você tiver usado um Olá scripts tooconfigure saudação do servidor de relatório, você poderá ignorar esta seção. script Hello incluída uma porta de firewall etapa tooopen hello. padrão de saudação era a porta 80 para HTTP e 443 para HTTPS.
> 
> 

tooconnect remotamente tooReport Manager ou Olá relatório Server na máquina virtual de saudação, um ponto de extremidade TCP é necessária no hello VM. É necessário tooopen Olá mesma porta no firewall da VM Olá. ponto de extremidade de saudação foi criado quando Olá VM foi provisionada.

Esta seção fornece informações básicas sobre como tooopen Olá porta do firewall. Para saber mais, consulte [Configurar um firewall para acesso ao servidor de relatório](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Se você usou o servidor de relatório do hello script tooconfigure hello, você poderá ignorar esta seção. script Hello incluída uma porta de firewall etapa tooopen hello.
> 
> 

Se você configurou uma porta privada para HTTPS diferente de 443, modifique Olá script a seguir apropriadamente. porta tooopen **443** no hello Firewall do Windows, conclua o seguinte hello:

1. Abra uma janela do Windows PowerShell com privilégios administrativos.
2. Se você usou uma porta diferente de 443 ao configurar o ponto de extremidade HTTPS de saudação em Olá VM, atualizar porta Olá Olá comando a seguir e, em seguida, execute o comando de saudação:
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Quando o comando Olá for concluído, **Okey** é exibido no prompt de comando hello.

tooverify que porta Olá é aberta, abra uma janela de Windows PowerShell e a execução Olá comando a seguir:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Verificar a configuração de saudação
tooverify a funcionalidade do servidor de relatório básico hello está funcionando agora, abra seu navegador com privilégios administrativos e, em seguida, procura toohello seguinte relatório Gerenciador de relatórios do servidor ad URLS:

* Na VM do hello, procure toohello URL do servidor de relatório:
  
        http://localhost/reportserver
* Na VM do hello, procure toohello URL do Gerenciador de relatórios:
  
        http://localhost/Reports
* No computador local, navegue toohello **remoto** Gerenciador de relatórios em Olá VM. Atualize o nome de DNS Olá Olá seguinte exemplo conforme apropriado. Quando for solicitada uma senha, use credenciais de administrador de saudação criado quando Olá VM foi provisionada. nome de usuário Hello está em Olá [domínio]\[nome de usuário] formato, onde o domínio de saudação é o nome do computador VM hello, por exemplo ssrsnativecloud\testuser. Se você não estiver usando HTTP**S**, remover Olá **s** na URL de saudação. Consulte a próxima seção Olá para obter informações sobre como criar usuários adicionais na VM.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* No computador local, procure toohello URL do servidor de relatório remoto. Atualize o nome de DNS Olá Olá seguinte exemplo conforme apropriado. Se você não estiver usando HTTPS, remova s Olá Olá URL.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Criar usuários e atribuir funções
Depois de configurar e verificar a saudação de servidor de relatório, uma tarefa administrativa comum é toocreate um ou mais usuários e atribuir usuários a funções de serviços tooReporting. Para obter mais informações, consulte o seguinte hello:

* [Criar uma conta de usuário local](https://technet.microsoft.com/library/cc770642.aspx)
* [Conceder acesso ao usuário tooa o servidor de relatório (Gerenciador de relatórios)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Criar e gerenciar atribuições de função](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate e publicar relatórios toohello Máquina Virtual do Azure
Olá tabela a seguir resume alguns dos relatórios existentes do hello opções toopublish disponíveis de um servidor de relatório local computador toohello hospedado em Olá Máquina Virtual do Microsoft Azure:

* **Script RS.exe**: itens de relatório Use RS.exe script toocopy do e tooyour de servidor de relatório existente Máquina Virtual do Microsoft Azure. Para obter mais informações, consulte a seção de hello "tooNative de modo nativo – modo de máquina Virtual do Microsoft Azure" em [Sample Reporting Services rs.exe Script tooMigrate conteúdo entre servidores de relatório](https://msdn.microsoft.com/library/dn531017.aspx).
* **Construtor de relatórios**: máquina virtual de saudação inclui Olá clique-uma vez a versão do construtor de relatórios do Microsoft SQL Server. saudação de construtor relatório toostart primeira vez na máquina virtual de saudação:
  
  1. Inicie o navegador com privilégios administrativos.
  2. Procurar tooreport manager na máquina virtual de saudação e clique em **Report Builder** na faixa de opções de saudação.
     
     Para saber mais, consulte [Instalando, Desinstalando e Dando Suporte ao Construtor de Relatórios](https://technet.microsoft.com/library/dd207038.aspx).
* **SQL Server Data Tools: VM**: se você criou Olá VM com o SQL Server 2012, SQL Server Data Tools está instalado na máquina virtual de saudação e pode ser usado toocreate **projetos do servidor de relatório** e relatórios sobre Olá virtual máquina. SQL Server Data Tools pode publicar o servidor de relatório de toohello Olá relatórios na máquina virtual de saudação.
  
    Se você criou Olá VM com o SQL server 2014, você pode instalar o SQL Server Data Tools - BI para visual Studio. Para obter mais informações, consulte o seguinte hello:
  
  * [Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools e SQL Server Business Intelligence (SSDT-BI)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools: Remoto**: no computador local, crie um projeto do Reporting Services no SQL Server Data Tools que contenha os relatórios do Reporting Services. Configure projeto Olá toohello tooconnect URL do serviço web.
  
    ![propriedades de projeto ssdt para projeto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Usar script**: usar o conteúdo do servidor de relatório de toocopy de script. Para obter mais informações, consulte [Sample Reporting Services rs.exe Script tooMigrate conteúdo entre servidores de relatório](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Minimizar o custo se você não estiver usando Olá VM
> [!NOTE]
> toominimize encargos para suas máquinas virtuais do Azure quando não estiver em uso, desligue Olá VM de saudação portal clássico do Azure. Se você usar opções de energia do Windows hello dentro de um tooshut VM para baixo Olá VM, você ainda será cobrado Olá mesmo valor para Olá VM. tooreduce encargos, você precisa tooshut inativo saudação VM no portal clássico do Azure de saudação. Se você não precisar mais Olá VM, lembre-se de toodelete Olá VM e Olá encargos de armazenamento de tooavoid de arquivos. vhd associado. Para obter mais informações, consulte a seção de saudação perguntas Frequentes em [detalhes de preços de máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Mais informações
### <a name="resources"></a>Recursos
* Para obter conteúdo semelhante relacionado a implantação de servidor único tooa do Business Intelligence do SQL Server e SharePoint 2013, consulte [tooCreate de usar o Windows PowerShell uma VM do Azure com SQL Server BI e SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* Para tooa relacionado de conteúdo semelhante a implantação de vários servidores de Business Intelligence do SQL Server e SharePoint 2013, consulte [implantar o SQL Server Business Intelligence em máquinas virtuais Azure](https://msdn.microsoft.com/library/dn321998.aspx).
* Para obter informações gerais relacionadas toodeployments do SQL Server Business Intelligence em máquinas de virtuais do Azure, consulte [SQL Server Business Intelligence em máquinas virtuais Azure](virtual-machines-windows-classic-ps-sql-bi.md).
* Para obter mais informações sobre o custo de saudação de encargos de computação do Azure, consulte o guia de máquinas virtuais de saudação do [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Conteúdo da comunidade
* Para obter instruções passo a passo sobre como toocreate um modo nativo do Reporting Services servidor de relatório sem usar o script, consulte [hospedando SQL Reporting Service na máquina Virtual Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Recursos de tooother links para o SQL Server em VMs do Azure
[Visão geral do SQL Server em máquinas virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

