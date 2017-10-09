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
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="7410f-103">Configurar um aplicativo LOB baseado na Web em uma nuvem híbrida para teste</span><span class="sxs-lookup"><span data-stu-id="7410f-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="7410f-104">Este tópico explica a criação de um ambiente de nuvem híbrida simulado para testar um aplicativo LOB (linha de negócios) baseado na Web, hospedado no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7410f-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="7410f-105">Aqui está a configuração resultante hello.</span><span class="sxs-lookup"><span data-stu-id="7410f-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="7410f-106">Essa configuração consiste em:</span><span class="sxs-lookup"><span data-stu-id="7410f-106">This configuration consists of:</span></span>

* <span data-ttu-id="7410f-107">Uma rede local simulada hospedada no Azure (Olá TestLab VNet).</span><span class="sxs-lookup"><span data-stu-id="7410f-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="7410f-108">Uma rede virtual entre locais hospedada no Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="7410f-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="7410f-109">Uma conexão VPN de VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="7410f-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="7410f-110">Um servidor LOB baseados na web, o SQL server e o controlador de domínio secundário na rede virtual do hello TestVNET.</span><span class="sxs-lookup"><span data-stu-id="7410f-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="7410f-111">Esta configuração proporciona uma base e um ponto de partida comum com os quais é possível:</span><span class="sxs-lookup"><span data-stu-id="7410f-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="7410f-112">Desenvolver e testar aplicativos LOB hospedados no IIS (Serviços de Informações da Internet) com um back-end de banco de dados do SQL Server 2014 no Azure.</span><span class="sxs-lookup"><span data-stu-id="7410f-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="7410f-113">Realizar testes dessa carga de trabalho simulada de TI baseada em nuvem híbrida.</span><span class="sxs-lookup"><span data-stu-id="7410f-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="7410f-114">Há três toosetting principais fases esse ambiente de teste de nuvem híbrida:</span><span class="sxs-lookup"><span data-stu-id="7410f-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="7410f-115">Configure o ambiente de nuvem híbrida simulada hello.</span><span class="sxs-lookup"><span data-stu-id="7410f-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="7410f-116">Configure o computador do SQL server (SQL1) hello.</span><span class="sxs-lookup"><span data-stu-id="7410f-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="7410f-117">Configure servidor LOB hello (LOB1).</span><span class="sxs-lookup"><span data-stu-id="7410f-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="7410f-118">Essa carga de trabalho requer uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7410f-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="7410f-119">Se você tiver uma assinatura do MSDN ou do Visual Studio, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="7410f-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="7410f-120">Para obter um exemplo de um aplicativo LOB hospedado no Azure de produção, consulte Olá **linha de aplicativos de negócios** projeto de arquitetura em [especificações técnicas e diagramas de arquitetura de Software do Microsoft](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="7410f-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="7410f-121">Etapa 1: Configurar o ambiente de nuvem híbrida simulada Olá</span><span class="sxs-lookup"><span data-stu-id="7410f-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="7410f-122">Criar hello [ambiente de teste de nuvem híbrida simulada](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7410f-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7410f-123">Como esse ambiente de teste não exigem a presença de saudação do servidor de saudação APP1 na sub-rede da rede corporativa de saudação, você pode desligá-lo agora.</span><span class="sxs-lookup"><span data-stu-id="7410f-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="7410f-124">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="7410f-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="7410f-125">Etapa 2: Configurar o computador do SQL server (SQL1) Olá</span><span class="sxs-lookup"><span data-stu-id="7410f-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="7410f-126">De Olá portal do Azure, inicie o computador de DC2 de saudação se necessário.</span><span class="sxs-lookup"><span data-stu-id="7410f-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="7410f-127">Em seguida, crie uma máquina virtual para o SQL1 com estes comandos em um prompt de comando do Azure PowerShell em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="7410f-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="7410f-128">Toorunning anterior desses comandos, preencha Olá valores de variáveis e remover hello < e > caracteres.</span><span class="sxs-lookup"><span data-stu-id="7410f-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

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

<span data-ttu-id="7410f-129">Use Olá tooSQL1 tooconnect portal do Azure usando a conta de administrador local de saudação do SQL1.</span><span class="sxs-lookup"><span data-stu-id="7410f-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="7410f-130">Em seguida, configure os testes de conectividade básica do tooallow de regras de Firewall do Windows e tráfego do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7410f-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="7410f-131">Em um prompt de comando com nível de administrador do Windows PowerShell no SQL1, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="7410f-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="7410f-132">comando de ping Olá deve resultar em quatro respostas bem-sucedidas do endereço IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="7410f-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="7410f-133">Em seguida, adicione Olá disco de dados extra no SQL1 como um novo volume com a letra da unidade Olá f:.</span><span class="sxs-lookup"><span data-stu-id="7410f-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="7410f-134">No painel esquerdo de saudação do Gerenciador do servidor, clique em **serviços de arquivo e armazenamento**e, em seguida, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="7410f-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="7410f-135">No painel de conteúdo de saudação em Olá **discos** de grupo, clique em **disco 2** (com hello **partição** definido muito**desconhecido**).</span><span class="sxs-lookup"><span data-stu-id="7410f-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="7410f-136">Clique em **Tarefas** e, em seguida, em **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="7410f-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="7410f-137">Na saudação antes de começar a página do Assistente de novo Volume de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="7410f-138">Na página de disco e servidor de saudação selecione hello, clique em **disco 2**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="7410f-139">Quando solicitado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7410f-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="7410f-140">No hello especificar tamanho de saudação da página de volume hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="7410f-141">Na saudação atribuir tooa unidade pasta ou letra da página, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="7410f-142">Na página de configurações do sistema do arquivo selecione hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="7410f-143">Na página Olá confirmar seleções, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="7410f-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="7410f-144">Ao concluir, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="7410f-144">When complete, click **Close**.</span></span>

<span data-ttu-id="7410f-145">Execute esses comandos no prompt de comando do Windows PowerShell Olá no SQL1:</span><span class="sxs-lookup"><span data-stu-id="7410f-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="7410f-146">Em seguida, ingresse em domínio de CORP Windows Server Active Directory do SQL1 toohello com esses comandos no prompt do Windows PowerShell Olá no SQL1.</span><span class="sxs-lookup"><span data-stu-id="7410f-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="7410f-147">Usar conta Olá CORP\User1 quando for solicitado credenciais de conta de domínio toosupply para Olá **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="7410f-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="7410f-148">Após a reinicialização, use Olá tooconnect portal do Azure tooSQL1 *com conta de administrador local de saudação do SQL1*.</span><span class="sxs-lookup"><span data-stu-id="7410f-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="7410f-149">Em seguida, configure a unidade do SQL Server 2014 toouse Olá f: para novos bancos de dados e permissões de conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7410f-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="7410f-150">Na tela de início do hello, digite **gerenciamento do SQL Server**e, em seguida, clique em **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="7410f-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="7410f-151">Em **conectar tooServer**, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="7410f-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="7410f-152">No painel de árvore do Pesquisador de objetos hello, clique com botão direito **SQL1**e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="7410f-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="7410f-153">Em Olá **propriedades do servidor** janela, clique em **configurações de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="7410f-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="7410f-154">Localizar Olá **locais padrão do banco de dados** e definir estes valores:</span><span class="sxs-lookup"><span data-stu-id="7410f-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="7410f-155">Para **dados**, digite o caminho Olá **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="7410f-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="7410f-156">Para **Log**, digite o caminho Olá **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="7410f-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="7410f-157">Para **Backup**, digite o caminho Olá **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="7410f-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="7410f-158">Aviso: somente novos bancos de dados usam esses locais.</span><span class="sxs-lookup"><span data-stu-id="7410f-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="7410f-159">Clique em Olá **Okey** tooclose janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="7410f-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="7410f-160">Em Olá **Pesquisador de objetos** painel de árvore, abra **segurança**.</span><span class="sxs-lookup"><span data-stu-id="7410f-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="7410f-161">Clique com o botão direito do mouse em **Logons** e clique em **Novo Logon**.</span><span class="sxs-lookup"><span data-stu-id="7410f-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="7410f-162">Em **Nome de Logon**, digite **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="7410f-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="7410f-163">Em Olá **funções de servidor** , clique em **sysadmin**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="7410f-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="7410f-164">Feche o Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="7410f-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="7410f-165">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="7410f-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="7410f-166">Etapa 3: Configurar o servidor LOB do hello (LOB1)</span><span class="sxs-lookup"><span data-stu-id="7410f-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="7410f-167">Primeiro, crie uma máquina virtual para LOB1 com esses comandos no prompt de comando do PowerShell do Azure Olá no computador local.</span><span class="sxs-lookup"><span data-stu-id="7410f-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

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

<span data-ttu-id="7410f-168">Em seguida, use Olá tooconnect portal do Azure tooLOB1 com credenciais de saudação da conta de administrador local de saudação do LOB1.</span><span class="sxs-lookup"><span data-stu-id="7410f-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="7410f-169">Em seguida, configure um tráfego de tooallow de regra de Firewall do Windows para testar a conectividade básica.</span><span class="sxs-lookup"><span data-stu-id="7410f-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="7410f-170">Em um prompt de comando com nível de administrador do Windows PowerShell no LOB1, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="7410f-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="7410f-171">comando de ping Olá deve resultar em quatro respostas bem-sucedidas do endereço IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="7410f-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="7410f-172">Em seguida, ingresse em domínio de CORP Active Directory de toohello LOB1 com esses comandos no prompt do Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7410f-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="7410f-173">Usar conta Olá CORP\User1 quando for solicitado credenciais de conta de domínio toosupply para Olá **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="7410f-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="7410f-174">Após a reinicialização, use Olá tooconnect portal do Azure tooLOB1 com hello corp/User1 conta e senha.</span><span class="sxs-lookup"><span data-stu-id="7410f-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="7410f-175">Em seguida, configure o LOB1 para IIS e teste o acesso do CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="7410f-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="7410f-176">No Gerenciador de Servidores, clique em **Adicionar funções e recursos**.</span><span class="sxs-lookup"><span data-stu-id="7410f-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="7410f-177">Em Olá **antes de começar a** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="7410f-178">Em Olá **Selecionar tipo de instalação** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="7410f-179">Em Olá **Selecionar servidor de destino** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="7410f-180">Em Olá **funções de servidor** , clique em **servidor Web (IIS)** na lista de saudação do **funções**.</span><span class="sxs-lookup"><span data-stu-id="7410f-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="7410f-181">Quando solicitado, clique em **Adicionar Recursos** e depois em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="7410f-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="7410f-182">Em Olá **selecionar recursos** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="7410f-183">Em Olá **servidor Web (IIS)** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="7410f-184">Em Olá **selecionar serviços de função** página, selecione ou desmarque caixas de seleção Olá serviços Olá necessários para testar seu aplicativo de LOB e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7410f-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="7410f-185">Em Olá **confirmar seleções de instalação** , clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="7410f-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="7410f-186">Aguarde a conclusão da instalação de saudação de componentes e, em seguida, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="7410f-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="7410f-187">De Olá portal do Azure, conecte o computador de CLIENT1 de toohello com credenciais de conta Olá corp/User1 e, em seguida, inicie o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="7410f-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="7410f-188">Na barra de endereços do hello, digite **http://lob1/** e pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="7410f-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="7410f-189">Você verá a página saudação padrão IIS 8 da web.</span><span class="sxs-lookup"><span data-stu-id="7410f-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="7410f-190">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="7410f-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="7410f-191">Esse ambiente agora está pronto para você toodeploy seu aplicativo baseado na web sobre a funcionalidade LOB1 e teste de CLIENT1 na sub-rede da rede corporativa de saudação.</span><span class="sxs-lookup"><span data-stu-id="7410f-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="7410f-192">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="7410f-192">Next step</span></span>
* <span data-ttu-id="7410f-193">Adicionar uma nova máquina virtual usando Olá [portal do Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7410f-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

