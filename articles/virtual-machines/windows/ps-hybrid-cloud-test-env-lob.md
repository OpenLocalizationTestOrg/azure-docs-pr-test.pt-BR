---
title: "Ambiente de teste de aplicativos de LOB (linha de negócios ) | Microsoft Docs"
description: "Aprenda a criar um aplicativo de linha de negócios baseado na Web em um ambiente de nuvem híbrida para testes profissionais de TI ou testes de desenvolvimento."
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
ms.openlocfilehash: 8e9a380458bfede80ed0fc1ee7e62b0caec09501
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="e479b-103">Configurar um aplicativo LOB baseado na Web em uma nuvem híbrida para teste</span><span class="sxs-lookup"><span data-stu-id="e479b-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="e479b-104">Este tópico explica a criação de um ambiente de nuvem híbrida simulado para testar um aplicativo LOB (linha de negócios) baseado na Web, hospedado no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e479b-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="e479b-105">Veja abaixo a configuração resultante.</span><span class="sxs-lookup"><span data-stu-id="e479b-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="e479b-106">Essa configuração consiste em:</span><span class="sxs-lookup"><span data-stu-id="e479b-106">This configuration consists of:</span></span>

* <span data-ttu-id="e479b-107">Uma rede local simulada hospedada no Azure (a VNet TestLab).</span><span class="sxs-lookup"><span data-stu-id="e479b-107">A simulated on-premises network hosted in Azure (the TestLab VNet).</span></span>
* <span data-ttu-id="e479b-108">Uma rede virtual entre locais hospedada no Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="e479b-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="e479b-109">Uma conexão VPN de VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="e479b-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="e479b-110">Um servidor LOB baseado na Web, um SQL Server e um controlador de domínio secundário na rede virtual TestVNET.</span><span class="sxs-lookup"><span data-stu-id="e479b-110">A web-based LOB server, SQL server, and secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="e479b-111">Esta configuração proporciona uma base e um ponto de partida comum com os quais é possível:</span><span class="sxs-lookup"><span data-stu-id="e479b-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="e479b-112">Desenvolver e testar aplicativos LOB hospedados no IIS (Serviços de Informações da Internet) com um back-end de banco de dados do SQL Server 2014 no Azure.</span><span class="sxs-lookup"><span data-stu-id="e479b-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="e479b-113">Realizar testes dessa carga de trabalho simulada de TI baseada em nuvem híbrida.</span><span class="sxs-lookup"><span data-stu-id="e479b-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="e479b-114">Há três fases principais para configurar esse ambiente de teste de nuvem híbrida:</span><span class="sxs-lookup"><span data-stu-id="e479b-114">There are three major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="e479b-115">Configurar um ambiente de nuvem híbrida simulado.</span><span class="sxs-lookup"><span data-stu-id="e479b-115">Set up the simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="e479b-116">Configurar o computador do servidor SQL (SQL1).</span><span class="sxs-lookup"><span data-stu-id="e479b-116">Configure the SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="e479b-117">Configurar o servidor LOB (LOB1).</span><span class="sxs-lookup"><span data-stu-id="e479b-117">Configure the LOB server (LOB1).</span></span>

<span data-ttu-id="e479b-118">Essa carga de trabalho requer uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e479b-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="e479b-119">Se você tiver uma assinatura do MSDN ou do Visual Studio, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="e479b-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="e479b-120">Para obter um exemplo de um aplicativo LOB de produção hospedado no Azure, consulte o plano gráfico da arquitetura de **Aplicativos de linha de negócios** em [Diagramas e planos gráficos de arquitetura de software Microsoft](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="e479b-120">For an example of a production LOB application hosted in Azure, see the **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-the-simulated-hybrid-cloud-environment"></a><span data-ttu-id="e479b-121">Fase 1: Configurar um ambiente de nuvem híbrida simulado</span><span class="sxs-lookup"><span data-stu-id="e479b-121">Phase 1: Set up the simulated hybrid cloud environment</span></span>
<span data-ttu-id="e479b-122">Crie o [ambiente de teste de nuvem híbrida simulado](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e479b-122">Create the [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e479b-123">Como esse ambiente de teste não exige a presença do servidor APP1 na sub-rede Corpnet, você pode desligá-lo por enquanto.</span><span class="sxs-lookup"><span data-stu-id="e479b-123">Because this test environment does not require the presence of the APP1 server on the Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="e479b-124">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="e479b-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-the-sql-server-computer-sql1"></a><span data-ttu-id="e479b-125">Fase 2: Configurar o computador do servidor SQL (SQL1)</span><span class="sxs-lookup"><span data-stu-id="e479b-125">Phase 2: Configure the SQL server computer (SQL1)</span></span>
<span data-ttu-id="e479b-126">No portal do Azure, inicie o computador DC2, se necessário.</span><span class="sxs-lookup"><span data-stu-id="e479b-126">From the Azure portal, start the DC2 computer if needed.</span></span>

<span data-ttu-id="e479b-127">Em seguida, crie uma máquina virtual para o SQL1 com estes comandos em um prompt de comando do Azure PowerShell em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="e479b-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="e479b-128">Antes de executar estes comandos, preencha os valores variáveis e remova os caracteres < e >.</span><span class="sxs-lookup"><span data-stu-id="e479b-128">Prior to running these commands, fill in the variable values and remove the < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<the Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type the name and password of the local administrator account for the SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="e479b-129">Use o portal do Azure para se conectar ao SQL1 usando a conta de administrador local do SQL1.</span><span class="sxs-lookup"><span data-stu-id="e479b-129">Use the Azure portal to connect to SQL1 using the local administrator account of SQL1.</span></span>

<span data-ttu-id="e479b-130">Em seguida, configure regras de Firewall do Windows para permitir testes de conectividade básica e o tráfego do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e479b-130">Next, configure Windows Firewall rules to allow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="e479b-131">Em um prompt de comando com nível de administrador do Windows PowerShell no SQL1, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="e479b-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="e479b-132">O comando ping deve resultar em quatro respostas bem-sucedidas do endereço IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="e479b-132">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="e479b-133">Em seguida, adicione o disco de dados extra no SQL1 como um novo volume com a letra de unidade F:.</span><span class="sxs-lookup"><span data-stu-id="e479b-133">Next, add the extra data disk on SQL1 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="e479b-134">No painel esquerdo do Gerenciador do Servidor, clique em **Serviços de Arquivo e Armazenamento** e, em seguida, clique em **Discos**.</span><span class="sxs-lookup"><span data-stu-id="e479b-134">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="e479b-135">No painel de conteúdo, no grupo **Discos**, clique em **disco 2** (com a **Partição** definida como **Desconhecida**).</span><span class="sxs-lookup"><span data-stu-id="e479b-135">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="e479b-136">Clique em **Tarefas** e, em seguida, em **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="e479b-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="e479b-137">Na página Antes de começar do Assistente de Novo Volume, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-137">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="e479b-138">Na página Selecione o servidor e o disco, clique em **Disco 2** e, em seguida, em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-138">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="e479b-139">Quando solicitado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e479b-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="e479b-140">Na página Especifique o tamanho do volume, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-140">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="e479b-141">Na página Atribuir a uma letra da unidade ou pasta, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-141">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="e479b-142">Na página Selecionar configurações do sistema de arquivos, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-142">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="e479b-143">Na página Confirmar seleções, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-143">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="e479b-144">Ao concluir, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-144">When complete, click **Close**.</span></span>

<span data-ttu-id="e479b-145">Execute estes comandos no prompt de comando do Windows PowerShell no SQL1:</span><span class="sxs-lookup"><span data-stu-id="e479b-145">Run these commands at the Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="e479b-146">Em seguida, integre o SQL1 ao domínio CORP do Windows Server Active Directory com estes comandos no prompt do Windows PowerShell no SQL1.</span><span class="sxs-lookup"><span data-stu-id="e479b-146">Next, join SQL1 to the CORP Windows Server Active Directory domain with these commands at the Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="e479b-147">Use a conta CORP\User1 quando for solicitado a fornecer credenciais da conta de domínio para o comando **Add-Computer**.</span><span class="sxs-lookup"><span data-stu-id="e479b-147">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="e479b-148">Após a reinicialização, use o portal do Azure para se conectar ao SQL1 *com a conta de administrador local do SQL1*.</span><span class="sxs-lookup"><span data-stu-id="e479b-148">After restarting, use the Azure portal to connect to SQL1 *with the local administrator account of SQL1*.</span></span>

<span data-ttu-id="e479b-149">Em seguida, configure o SQL Server 2014 para usar a unidade F: para novos bancos de dados e permissões de conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="e479b-149">Next, configure SQL Server 2014 to use the F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="e479b-150">Na tela inicial, digite **Gerenciamento do SQL Server** e, em seguida, clique em **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="e479b-150">From the Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="e479b-151">Em **Conectar ao Servidor**, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-151">In **Connect to Server**, click **Connect**.</span></span>
3. <span data-ttu-id="e479b-152">No painel de árvore do Pesquisador de Objetos, clique com o botão direito do mouse em **SQL1**e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e479b-152">In the Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="e479b-153">Na janela **Propriedades do Servidor**, clique em **Configurações de Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="e479b-153">In the **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="e479b-154">Localize os **Locais padrão de banco de dados** e defina estes valores:</span><span class="sxs-lookup"><span data-stu-id="e479b-154">Locate the **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="e479b-155">Para **Dados**, digite o caminho **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="e479b-155">For **Data**, type the path **f:\Data**.</span></span>
   * <span data-ttu-id="e479b-156">Para **Log**, digite o caminho **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="e479b-156">For **Log**, type the path **f:\Log**.</span></span>
   * <span data-ttu-id="e479b-157">Para **Backup**, digite o caminho **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="e479b-157">For **Backup**, type the path **f:\Backup**.</span></span>
   * <span data-ttu-id="e479b-158">Aviso: somente novos bancos de dados usam esses locais.</span><span class="sxs-lookup"><span data-stu-id="e479b-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="e479b-159">Clique em **OK** para fechar a janela.</span><span class="sxs-lookup"><span data-stu-id="e479b-159">Click the **OK** to close the window.</span></span>
7. <span data-ttu-id="e479b-160">No painel de árvore do **Pesquisador de Objetos**, abra **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="e479b-160">In the **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="e479b-161">Clique com o botão direito do mouse em **Logons** e clique em **Novo Logon**.</span><span class="sxs-lookup"><span data-stu-id="e479b-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="e479b-162">Em **Nome de Logon**, digite **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="e479b-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="e479b-163">Na página **Funções de Servidor**, clique em **sysadmin** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e479b-163">On the **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="e479b-164">Feche o Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e479b-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="e479b-165">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="e479b-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-the-lob-server-lob1"></a><span data-ttu-id="e479b-166">Fase 3: Configurar o servidor LOB (LOB1)</span><span class="sxs-lookup"><span data-stu-id="e479b-166">Phase 3: Configure the LOB server (LOB1)</span></span>
<span data-ttu-id="e479b-167">Primeiro, crie uma máquina virtual para LOB1 com estes comandos no prompt de comando do Azure PowerShell em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="e479b-167">First, create a virtual machine for LOB1 with these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="e479b-168">Em seguida, use o portal do Azure para se conectar ao LOB1 com as credenciais da conta de administrador local de LOB1.</span><span class="sxs-lookup"><span data-stu-id="e479b-168">Next, use the Azure portal to connect to LOB1 with the credentials of the local administrator account of LOB1.</span></span>

<span data-ttu-id="e479b-169">Em seguida, configure uma regra do Firewall do Windows para permitir o tráfego e testar a conectividade básica.</span><span class="sxs-lookup"><span data-stu-id="e479b-169">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="e479b-170">Em um prompt de comando com nível de administrador do Windows PowerShell no LOB1, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="e479b-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="e479b-171">O comando ping deve resultar em quatro respostas bem-sucedidas do endereço IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="e479b-171">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="e479b-172">Em seguida, integre a LOB1 ao domínio CORP do Active Directory com estes comandos no prompt do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e479b-172">Next, join LOB1 to the CORP Active Directory domain with these commands at the Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="e479b-173">Use a conta CORP\User1 quando for solicitado a fornecer credenciais da conta de domínio para o comando **Add-Computer**.</span><span class="sxs-lookup"><span data-stu-id="e479b-173">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="e479b-174">Após a reinicialização, use o portal do Azure para conectar-se ao LOB1 com a conta e senha CORP\User1.</span><span class="sxs-lookup"><span data-stu-id="e479b-174">After restarting, use the Azure portal to connect to LOB1 with the CORP\User1 account and password.</span></span>

<span data-ttu-id="e479b-175">Em seguida, configure o LOB1 para IIS e teste o acesso do CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="e479b-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="e479b-176">No Gerenciador de Servidores, clique em **Adicionar funções e recursos**.</span><span class="sxs-lookup"><span data-stu-id="e479b-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="e479b-177">Na página **Antes de Começar**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-177">On the **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="e479b-178">Na página **Selecionar tipo de instalação**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-178">On the **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="e479b-179">Na página **Selecionar servidor de destino**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-179">On the **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="e479b-180">Na página **Funções do servidor**, clique em **Servidor Web (IIS)** na lista **Funções**.</span><span class="sxs-lookup"><span data-stu-id="e479b-180">On the **Server roles** page, click **Web Server (IIS)** in the list of **Roles**.</span></span>
6. <span data-ttu-id="e479b-181">Quando solicitado, clique em **Adicionar Recursos** e depois em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="e479b-182">Na página **Selecionar recursos**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-182">On the **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="e479b-183">Na página **Servidor Web (IIS)**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-183">On the **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="e479b-184">Na página **Selecionar serviços da função**, marque ou desmarque as caixas de seleção dos serviços de que você precisa para testar seu aplicativo LOB e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-184">On the **Select role services** page, select or clear the check boxes for the services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="e479b-185">Na página **Confirmar seleções da instalação**, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-185">On the **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="e479b-186">Aguarde a conclusão da instalação dos componentes e clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="e479b-186">Wait until the installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="e479b-187">No portal do Azure, conecte-se ao computador CLIENT1 com as credenciais da conta CORP\User1 e inicie o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="e479b-187">From the Azure portal, connect to the CLIENT1 computer with the CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="e479b-188">Na barra de endereços, digite **http://lob1/** e pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="e479b-188">In the Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="e479b-189">Você verá a página da Web do IIS 8 padrão.</span><span class="sxs-lookup"><span data-stu-id="e479b-189">You should see the default IIS 8 web page.</span></span>

<span data-ttu-id="e479b-190">Esta é a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="e479b-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="e479b-191">Este ambiente agora está pronto para que você implante seu aplicativo baseado na Web no LOB1 e teste a funcionalidade do CLIENT1 na sub-rede Corpnet.</span><span class="sxs-lookup"><span data-stu-id="e479b-191">This environment is now ready for you to deploy your web-based application on LOB1 and test functionality from CLIENT1 on the Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="e479b-192">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="e479b-192">Next step</span></span>
* <span data-ttu-id="e479b-193">Adicionar uma nova máquina virtual usando o [portal do Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e479b-193">Add a new virtual machine using the [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

