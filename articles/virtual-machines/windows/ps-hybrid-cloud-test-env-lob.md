---
title: ambiente de teste de aplicativo aaaLOB | Microsoft Docs
description: "Saiba como toocreate baseado na web, a linha de aplicativos de negócios em um ambiente híbrido de nuvem ambiente para IT pro ou testes de desenvolvimento."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Configurar um aplicativo LOB baseado na Web em uma nuvem híbrida para teste
Este tópico explica a criação de um ambiente de nuvem híbrida simulado para testar um aplicativo LOB (linha de negócios) baseado na Web, hospedado no Microsoft Azure. Aqui está a configuração resultante hello.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Essa configuração consiste em:

* Uma rede local simulada hospedada no Azure (Olá TestLab VNet).
* Uma rede virtual entre locais hospedada no Azure (TestVNET).
* Uma conexão VPN de VNet para VNet.
* Um servidor LOB baseados na web, o SQL server e o controlador de domínio secundário na rede virtual do hello TestVNET.

Esta configuração proporciona uma base e um ponto de partida comum com os quais é possível:

* Desenvolver e testar aplicativos LOB hospedados no IIS (Serviços de Informações da Internet) com um back-end de banco de dados do SQL Server 2014 no Azure.
* Realizar testes dessa carga de trabalho simulada de TI baseada em nuvem híbrida.

Há três toosetting principais fases esse ambiente de teste de nuvem híbrida:

1. Configure o ambiente de nuvem híbrida simulada hello.
2. Configure o computador do SQL server (SQL1) hello.
3. Configure servidor LOB hello (LOB1).

Essa carga de trabalho requer uma assinatura do Azure. Se você tiver uma assinatura do MSDN ou do Visual Studio, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Para obter um exemplo de um aplicativo LOB hospedado no Azure de produção, consulte Olá **linha de aplicativos de negócios** projeto de arquitetura em [especificações técnicas e diagramas de arquitetura de Software do Microsoft](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Etapa 1: Configurar o ambiente de nuvem híbrida simulada Olá
Criar hello [ambiente de teste de nuvem híbrida simulada](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Como esse ambiente de teste não exigem a presença de saudação do servidor de saudação APP1 na sub-rede da rede corporativa de saudação, você pode desligá-lo agora.

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Etapa 2: Configurar o computador do SQL server (SQL1) Olá
De Olá portal do Azure, inicie o computador de DC2 de saudação se necessário.

Em seguida, crie uma máquina virtual para o SQL1 com estes comandos em um prompt de comando do Azure PowerShell em seu computador local. Toorunning anterior desses comandos, preencha Olá valores de variáveis e remover hello < e > caracteres.

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Use Olá tooSQL1 tooconnect portal do Azure usando a conta de administrador local de saudação do SQL1.

Em seguida, configure os testes de conectividade básica do tooallow de regras de Firewall do Windows e tráfego do SQL Server. Em um prompt de comando com nível de administrador do Windows PowerShell no SQL1, execute estes comandos.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comando de ping Olá deve resultar em quatro respostas bem-sucedidas do endereço IP 192.168.0.4.

Em seguida, adicione Olá disco de dados extra no SQL1 como um novo volume com a letra da unidade Olá f:.

1. No painel esquerdo de saudação do Gerenciador do servidor, clique em **serviços de arquivo e armazenamento**e, em seguida, clique em **discos**.
2. No painel de conteúdo de saudação em Olá **discos** de grupo, clique em **disco 2** (com hello **partição** definido muito**desconhecido**).
3. Clique em **Tarefas** e, em seguida, em **Novo Volume**.
4. Na saudação antes de começar a página do Assistente de novo Volume de saudação, clique em **próximo**.
5. Na página de disco e servidor de saudação selecione hello, clique em **disco 2**e, em seguida, clique em **próximo**. Quando solicitado, clique em **OK**.
6. No hello especificar tamanho de saudação da página de volume hello, clique em **próximo**.
7. Na saudação atribuir tooa unidade pasta ou letra da página, clique em **próximo**.
8. Na página de configurações do sistema do arquivo selecione hello, clique em **próximo**.
9. Na página Olá confirmar seleções, clique em **criar**.
10. Ao concluir, clique em **Fechar**.

Execute esses comandos no prompt de comando do Windows PowerShell Olá no SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

Em seguida, ingresse em domínio de CORP Windows Server Active Directory do SQL1 toohello com esses comandos no prompt do Windows PowerShell Olá no SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Usar conta Olá CORP\User1 quando for solicitado credenciais de conta de domínio toosupply para Olá **Add-Computer** comando.

Após a reinicialização, use Olá tooconnect portal do Azure tooSQL1 *com conta de administrador local de saudação do SQL1*.

Em seguida, configure a unidade do SQL Server 2014 toouse Olá f: para novos bancos de dados e permissões de conta de usuário.

1. Na tela de início do hello, digite **gerenciamento do SQL Server**e, em seguida, clique em **SQL Server 2014 Management Studio**.
2. Em **conectar tooServer**, clique em **conectar**.
3. No painel de árvore do Pesquisador de objetos hello, clique com botão direito **SQL1**e, em seguida, clique em **propriedades**.
4. Em Olá **propriedades do servidor** janela, clique em **configurações de banco de dados**.
5. Localizar Olá **locais padrão do banco de dados** e definir estes valores: 
   * Para **dados**, digite o caminho Olá **f:\Data**.
   * Para **Log**, digite o caminho Olá **f:\Log**.
   * Para **Backup**, digite o caminho Olá **f:\Backup**.
   * Aviso: somente novos bancos de dados usam esses locais.
6. Clique em Olá **Okey** tooclose janela de saudação.
7. Em Olá **Pesquisador de objetos** painel de árvore, abra **segurança**.
8. Clique com o botão direito do mouse em **Logons** e clique em **Novo Logon**.
9. Em **Nome de Logon**, digite **CORP\User1**.
10. Em Olá **funções de servidor** , clique em **sysadmin**e, em seguida, clique em **Okey**.
11. Feche o Microsoft SQL Server Management Studio.

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Etapa 3: Configurar o servidor LOB do hello (LOB1)
Primeiro, crie uma máquina virtual para LOB1 com esses comandos no prompt de comando do PowerShell do Azure Olá no computador local.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Em seguida, use Olá tooconnect portal do Azure tooLOB1 com credenciais de saudação da conta de administrador local de saudação do LOB1.

Em seguida, configure um tráfego de tooallow de regra de Firewall do Windows para testar a conectividade básica. Em um prompt de comando com nível de administrador do Windows PowerShell no LOB1, execute estes comandos.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comando de ping Olá deve resultar em quatro respostas bem-sucedidas do endereço IP 192.168.0.4.

Em seguida, ingresse em domínio de CORP Active Directory de toohello LOB1 com esses comandos no prompt do Windows PowerShell hello.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Usar conta Olá CORP\User1 quando for solicitado credenciais de conta de domínio toosupply para Olá **Add-Computer** comando.

Após a reinicialização, use Olá tooconnect portal do Azure tooLOB1 com hello corp/User1 conta e senha.

Em seguida, configure o LOB1 para IIS e teste o acesso do CLIENT1.

1. No Gerenciador de Servidores, clique em **Adicionar funções e recursos**.
2. Em Olá **antes de começar a** , clique em **próximo**.
3. Em Olá **Selecionar tipo de instalação** , clique em **próximo**.
4. Em Olá **Selecionar servidor de destino** , clique em **próximo**.
5. Em Olá **funções de servidor** , clique em **servidor Web (IIS)** na lista de saudação do **funções**.
6. Quando solicitado, clique em **Adicionar Recursos** e depois em **Avançar**.
7. Em Olá **selecionar recursos** , clique em **próximo**.
8. Em Olá **servidor Web (IIS)** , clique em **próximo**.
9. Em Olá **selecionar serviços de função** página, selecione ou desmarque caixas de seleção Olá serviços Olá necessários para testar seu aplicativo de LOB e, em seguida, clique em **próximo**.
10. Em Olá **confirmar seleções de instalação** , clique em **instalar**.
11. Aguarde a conclusão da instalação de saudação de componentes e, em seguida, clique em **fechar**.
12. De Olá portal do Azure, conecte o computador de CLIENT1 de toohello com credenciais de conta Olá corp/User1 e, em seguida, inicie o Internet Explorer.
13. Na barra de endereços do hello, digite **http://lob1/** e pressione ENTER. Você verá a página saudação padrão IIS 8 da web.

Esta é a configuração atual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Esse ambiente agora está pronto para você toodeploy seu aplicativo baseado na web sobre a funcionalidade LOB1 e teste de CLIENT1 na sub-rede da rede corporativa de saudação.

## <a name="next-step"></a>Próxima etapa
* Adicionar uma nova máquina virtual usando Olá [portal do Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

