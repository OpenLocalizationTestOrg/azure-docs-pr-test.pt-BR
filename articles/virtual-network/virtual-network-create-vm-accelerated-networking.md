---
title: "aaaCreate uma máquina virtual do Azure com rede acelerado | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual com acelerado de rede."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Criar uma máquina virtual com Rede Acelerada

Neste tutorial, você aprenderá como toocreate uma máquina Virtual (VM) do Azure com acelerado em rede. A Rede Acelerada é GA para Windows e em uma Visualização Pública para distribuições específicas do Linux. Rede acelerado permite tooa de virtualização (SR-IOV) de e/s de raiz única VM, melhorando o desempenho de rede. Esse caminho de alto desempenho ignora o host de saudação do caminho de dados Olá reduzindo a latência, a variação e a utilização da CPU, para uso com cargas de trabalho mais exigentes de rede do hello em tipos VM com suporte. Olá a seguir mostra a imagem a comunicação entre duas máquinas virtuais (VM) com e sem conexão de rede rápida:

![Comparação](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Sem conexão de rede rápida, todo o tráfego de rede dentro e fora de saudação VM deve ignorar host hello e comutador hello. Olá ele proporciona imposição de política de todos os, tais como grupos de segurança de rede acessar listas de controle, isolamento e outro tráfego de toonetwork de serviços de rede virtualizado. toolearn mais sobre os comutadores virtuais, ler Olá [virtualização de rede do Hyper-V e o comutador virtual](https://technet.microsoft.com/library/jj945275.aspx) artigo.

Com a rede acelerada, tráfego de rede chega na interface de rede da VM hello (NIC) e é então encaminhado toohello VM. Aplica-se todas as políticas de rede que Olá comutador virtual sem rede acelerado são descarregados e aplicadas em hardware. Aplicação de política no hardware habilita Olá NIC tooforward tráfego de rede diretamente toohello VM, ignorando host hello e comutador hello, mantendo todas as política Olá ele aplicado no host de saudação.

Olá benefícios da rede acelerado se aplicam somente toohello que ele é habilitado na VM. Para obter melhores resultados de Olá, é ideal tooenable esse recurso em pelo menos duas VMs conectado toohello mesma rede Virtual do Azure (VNet). Ao se comunicar em VNets ou a conexão local, esse recurso tem uma latência de toooverall impacto mínimo.

> [!WARNING]
> Este Linux visualização pública pode não ter Olá são do mesmo nível de disponibilidade e confiabilidade como recursos em geral versão de disponibilidade. Olá recurso não tem suporte, pode ter restringido recursos e pode não estar disponível em todos os locais do Azure. Para notificações mais recentes de Olá em disponibilidade e o status desse recurso, verifique Olá página de atualizações de rede Virtual do Azure.

## <a name="benefits"></a>Benefícios
* **Reduzir a latência / superior pacotes por segundo (pps):** removendo Olá comutador do caminho de dados de saudação remove tempo de saudação pacotes gastam no host Olá para processamento de política e aumenta Olá número de pacotes que podem ser processadas em Olá VM.
* **Redução de tremulação:** switch Virtual processamento depende de quantidade de saudação de política que precisa toobe aplicado e Olá carga de trabalho de saudação da CPU que está fazendo o processamento de saudação. O descarregamento de hardware de toohello de imposição de política de saudação remove essa variação, oferecendo pacotes diretamente alterna toohello VM, removendo a comunicação Olá host tooVM e todas as interrupções de software e contexto.
* **Diminuir a utilização da CPU:** Bypassing Olá comutador no host Olá leva a utilização de CPU tooless para processamento do tráfego de rede.

## <a name="Limitations"></a>Limitações
Olá limitações a seguir existe ao usar esse recurso:

* **Criação de interface de rede:** rede acelerada só pode ser habilitada para uma NIC nova. Não pode ser habilitada para uma NIC existente.
* **Criação de VM:** A NIC com a rede acelerado habilitada pode somente ser anexado tooa VM quando hello VM é criada. Olá NIC não pode ser anexado tooan existente de VM.
* **Regiões:** VMs do Windows com rede acelerada são oferecidas na maioria das regiões do Azure. VMs do Linux com rede acelerada são oferecidas em várias regiões. regiões Olá esse recurso está disponível em expansão. Consulte o blog de atualizações de sistema de rede Virtual do Azure Olá abaixo para obter informações mais recentes de saudação.   
* **Sistemas operacionais com suporte:** Windows: Microsoft Windows Server 2012 R2 Datacenter e Windows Server 2016. Linux: Ubuntu Server 16.04 LTS com kernel 4.4.0-77 ou superior, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (publicado por "Rogue Wave Software").
* **Tamanho da VM:** tamanhos de instância com computação otimizada e de finalidade geral com oito ou mais núcleos. Para obter mais informações, consulte Olá [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM. Olá conjunto de tamanhos de instância VM com suporte será expandida em Olá futuras.
* **Implantação somente por meio do ARM (Azure Resource Manager):** a Rede Acelerada não está disponível para implantação por meio do ASM/RDFE.

Alterações toothese limitações são anunciadas pelo Olá [rede Virtual do Azure atualiza](https://azure.microsoft.com/updates/accelerated-networking-in-preview) página.

## <a name="create-a-windows-vm"></a>Criar uma VM do Windows
Você pode usar o hello portal do Azure ou Azure [PowerShell](#windows-powershell) toocreate Olá VM.

### <a name="windows-portal"></a>Portal

1. Em um navegador da Internet, abra hello Azure [portal](https://portal.azure.com) e entre com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. No portal de saudação, clique em **+ novo** > **de computação** > **Datacenter do Windows Server 2016**. 
3. Em Olá **Datacenter do Windows Server 2016** folha exibida, deixe *Gerenciador de recursos de* selecionado em **selecionar um modelo de implantação**e clique em **criar** .
4. Em Olá **Noções básicas de** folha que aparece, digite Olá valores a seguir, deixe Olá restantes opções padrão ou selecione ou insira seus próprios valores e clique em Olá **Okey** botão:

    |Configuração|Valor|
    |---|---|
    |Nome|MyVm|
    |Grupo de recursos|Deixe **Criar novo** selecionado e digite *MyResourceGroup*|
    |Local|Oeste dos EUA 2|

    Se você for novo tooAzure, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [locais](https://azure.microsoft.com/regions) (que também são chamadas de regiões tooas).
5. Em Olá **escolher um tamanho de** folha que aparece, digite *8* em Olá **mínimo de núcleos** caixa e, em seguida, clique em **exibir todos os**.
6. Clique em **DS4_V2 padrão**, ou qualquer suporte a VM, e clique em Olá **selecione** botão.
7. Em hello **configurações** folha exibida, deixe todas as configurações como-é, exceto clique **habilitado** em **acelerado por rede**, clique Olá **Okey** botão. **Observação:** se, nas etapas anteriores, você selecionou valores de tamanho VM, o sistema operacional ou local que não estão listados na Olá [limitações](#Limitations) deste artigo, **Accelerated rede**não estiver visível.
8. Em Olá **resumo** folha que aparece, clique em Olá **Okey** botão. Criando Olá VM a partir do Azure. A criação da VM leva alguns minutos.
9. Olá tooinstall acelerado driver de rede para Windows, Olá concluir as etapas em Olá [configurar o Windows](#configure-windows) deste artigo.

### <a name="windows-powershell"></a>PowerShell
1. Instale a versão mais recente Olá de saudação do Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se você for novo tooAzure PowerShell, ler Olá [visão geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.
2. Iniciar uma sessão do PowerShell clicando o botão Iniciar do Windows hello, digitando **powershell**, em seguida, clicando em **PowerShell** Olá dos resultados da pesquisa.
3. Na janela do PowerShell, digite Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. No navegador, copie Olá script a seguir:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. Na janela do PowerShell, clique toopaste script de saudação e começar a executá-lo. Você será solicitado a informar um nome de usuário e senha. Use essas credenciais toolog no toohello VM ao conectar-se tooit na próxima etapa do hello. Se o script hello falha e você alterou os valores no script hello antes da execução, confirme valores hello usado para o tamanho da VM, sistema operacional, e local são listados no hello [limitações](#Limitations) deste artigo.
6. Olá tooinstall acelerado driver de rede para Windows, Olá concluir as etapas em Olá [configurar o Windows](#configure-windows) deste artigo.

### <a name="configure-windows"></a>Configurar Windows
Quando você criar hello VM no Azure, você deve instalar o driver de rede acelerado Olá para Windows. Antes de concluir Olá etapas a seguir, você deve ter uma VM do Windows criado com a rede acelerado usando qualquer Olá [portal](#windows-portal) ou [PowerShell](#windows-powershell) as etapas neste artigo. 

1. Em um navegador da Internet, abra hello Azure [portal](https://portal.azure.com) e entre com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *MyVm*. Quando **MyVm** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **MyVm** folha que aparece, clique em Olá **conectar** botão no canto superior esquerdo de saudação da folha de saudação. **Observação:** se **criando** for visível sob Olá **conectar** botão Azure ainda não foi concluída criando Olá VM. Clique em **conectar** somente depois que você não verá mais **criando** em Olá **conectar** botão.
4. Permitir Olá de toodownload seu navegador **MyVm.rdp** arquivo.  Após o download, clique em Olá arquivo tooopen-lo. 
5. Clique em Olá **conectar** botão Olá **Conexão de área de trabalho remota** caixa que aparece, informando que Olá Editor de conexão remota Olá não pode ser identificado.
6. Em Olá **a segurança do Windows** caixa que aparece, clique em **mais opções**, em seguida, clique em **usar uma conta diferente**. Digite hello nome de usuário e senha que você digitou na etapa 4, clique em Olá **Okey** botão.
7. Clique em Olá **Sim** botão na caixa de Conexão de área de trabalho remota Olá que aparece, informando que a identidade de saudação do computador remoto Olá não pode ser verificada.
8. Clique o botão Iniciar do Windows do hello e clique em **Gerenciador de dispositivos**. Expanda Olá **adaptadores de rede** nó. Confirme que Olá **adaptador de Ethernet de função Virtual Mellanox ConnectX-3** aparece, como mostrado na figura abaixo de saudação:
   
    ![Gerenciador de Dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. A Rede Acelerada agora está habilitada para sua VM.

## <a name="create-a-linux-vm"></a>Criar uma VM do Linux
Você pode usar o hello portal do Azure ou Azure [PowerShell](#linux-powershell) toocreate um Ubuntu ou SLES VM. Para VMs RHEL e CentOS, há um fluxo de trabalho diferente.  Consulte as instruções de saudação abaixo.

### <a name="linux-portal"></a>Portal
1. Registre-se para Olá acelerado de rede para a visualização de Linux completando as etapas 1 a 5 de saudação [criar uma VM do Linux - PowerShell](#linux-powershell) deste artigo.  Você não pode registrar para visualização de saudação no portal de saudação.
2. Concluir as etapas Olá em 1 a 8 [criar uma VM do Windows - portal](#windows-portal) deste artigo. Na etapa 2, clique em **Ubuntu Server 16.04 LTS**, em vez de **Windows Server 2016 Datacenter**. Para este tutorial, escolha toouse uma senha, em vez de uma chave SSH, embora para implantações de produção, você pode usar. Se **acelerado por rede** não aparece quando você concluir a etapa 7 da saudação [criar uma VM do Windows - portal](#windows-portal) seção deste artigo, é provável que uma saudação motivos a seguir:
    - Você não ainda foram registradas para a visualização de saudação. Confirme se o estado do registro é **registrado**, conforme explicado na etapa 4 do hello [criar uma VM do Linux - Powershell](#linux-powershell) deste artigo. **Observação:** se você participou da saudação acelerada de rede para a visualização de máquinas virtuais do Windows (seu nenhum toouse tooregister necessário mais acelerado de rede para máquinas virtuais do Windows), você não é registrados automaticamente para Olá Accelerated rede para Visualização de VMs do Linux. Você deve registrar para a rede de Accelerated Olá para VMs do Linux visualizar tooparticipate nele.
    - Você não selecionou um tamanho VM, o sistema operacional ou o local listado na Olá [limitações](#limitations) deste artigo.
3. Olá tooinstall acelerado driver de rede para Linux, Olá concluir as etapas em Olá [configurar Linux](#configure-linux) deste artigo.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>Se você criar VMs do Linux com redes acelerado em uma assinatura e, em seguida, tente toocreate uma VM do Windows com a rede acelerada em Olá mesma assinatura, Olá criação de VM do Windows pode falhar. Durante essa versão prévia, é recomendável testar VMs do Linux e do Windows com rede acelerada em assinaturas diferentes.
>

1. Instale a versão mais recente Olá de saudação do Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se você for novo tooAzure PowerShell, ler Olá [visão geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.
2. Iniciar uma sessão do PowerShell clicando o botão Iniciar do Windows hello, digitando **powershell**, em seguida, clicando em **PowerShell** Olá dos resultados da pesquisa.
3. Na janela do PowerShell, digite Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Registre-se para Olá acelerado de rede para o Azure preview Concluindo Olá etapas a seguir:
    - Enviar um email muito[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) com sua ID de assinatura do Azure e o uso pretendido. Aguarde um email de confirmação da Microsoft sobre sua assinatura ser habilitada.
    - Digite hello tooconfirm de comando que você está registrado para a visualização de saudação a seguir:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Não continue com a etapa 5 até **registrado** aparece no hello depois de inserir o comando anterior Olá de saída. A saída deve ter a aparência Olá seguir saída antes de continuar:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Se você participou da saudação acelerada de rede para a visualização de máquinas virtuais do Windows (seu nenhum toouse tooregister necessário mais acelerado de rede para máquinas virtuais do Windows), você não é registrados automaticamente para Olá acelerada de rede para a visualização de VMs do Linux. Você deve registrar para a rede de Accelerated Olá para VMs do Linux visualizar tooparticipate nele.
      >
5. No navegador, cópia Olá script a seguir substituindo Ubuntu ou SLES conforme desejado.  Novamente, o Redhat e o CentOS têm um fluxo de trabalho diferente, descrito abaixo:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. Na janela do PowerShell, clique toopaste script de saudação e começar a executá-lo. Você será solicitado a informar um nome de usuário e senha. Use essas credenciais toolog no toohello VM ao conectar-se tooit na próxima etapa do hello. Se o script hello falhar, confirme se:
    - Você está registrado para a visualização de hello, conforme explicado na etapa 4
    - Se você alterou o tamanho, tipo de sistema operacional ou valores do local no script hello VM antes da execução, que os valores hello estão listados na Olá [limitações](#Limitations) deste artigo.
7. Olá tooinstall acelerado driver de rede para Linux, Olá concluir as etapas em Olá [configurar Linux](#configure-linux) deste artigo.

### <a name="configure-linux"></a>Configurar Linux

Quando você criar hello VM no Azure, você deve instalar o driver de rede acelerado Olá para Linux. Antes de concluir Olá etapas a seguir, você deve ter uma VM do Linux criado com a rede acelerado usando qualquer Olá [portal](#linux-portal) ou [PowerShell](#linux-powershell) as etapas neste artigo. 

1. Em um navegador da Internet, abra hello Azure [portal](https://portal.azure.com) e entre com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Na parte superior de saudação do direito de toohello portal, Olá de saudação *pesquisar recursos* barra, clique em Olá **> _** ícone toostart um shell de nuvem Bash (visualização). Olá Bash nuvem shell painel aparece na parte inferior de saudação do portal hello e após alguns segundos, apresenta um  **username@Azure:~ $** prompt. Embora seja possível SSH toohello VM do seu computador, em vez do shell de nuvem Olá, instruções de saudação neste tutorial presumem que você está usando o shell de nuvem hello.
3. Na parte superior de saudação do portal hello, na caixa de saudação que contém o texto de saudação *pesquisar recursos*, tipo *MyVm*. Quando **MyVm** aparece nos resultados da pesquisa hello, clique nele.
4. Em Olá **MyVm** folha que aparece, clique em Olá **conectar** botão no canto superior esquerdo de saudação da folha de saudação. **Observação:** se **criando** for visível sob Olá **conectar** botão Azure ainda não foi concluída criando Olá VM. Clique em **conectar** somente depois que você não verá mais **criando** em Olá **conectar** botão.
5. Azure abre uma caixa informando Olá tooenter `ssh adminuser@<ipaddress>`. Digite este comando no hello nuvem shell (ou cópia de caixa de saudação apareceu na etapa 4 e cole-o no shell de nuvem toohello), em seguida, pressione Enter.
6. Insira **Sim** toohello pergunta solicitando que você se você quiser se conectar toocontinue, em seguida, pressione Enter.
7. Digite a senha de saudação inserido durante a criação de saudação VM. Uma vez fez logon com êxito no toohello VM, você verá um adminuser@MyVm:~ prompt$. Agora você está logado toohello VM por meio da sessão do shell de nuvem hello. **Observação:** as sessões de cloud shell atingem o tempo limite depois de 10 minutos de inatividade.

Neste ponto, instruções de saudação variam de acordo com distribuição Olá que você está usando. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. No prompt de hello, digite `uname -r` e confirmar versão Olá para:

    * O Ubuntu é "4.4.0-77-generic" ou superior
    * O SLES é "4.4.59-92.20-default" ou superior

2. Crie um vínculo entre o hello vNIC de rede padrão e vNIC rede Olá acelerado por execução de comandos Olá que seguem. Tráfego de rede usa Olá maior desempenho acelerada vNIC de rede, enquanto o título Olá garante que o tráfego de rede não seja interrompido em determinadas alterações de configuração.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Após executando o script hello, Olá VM será reiniciado depois de pausar a 60 segundos.
4. Uma vez Olá VM é reiniciada, reconecte tooit completando as etapas 5 a 7 novamente.
5. Executar Olá `ifconfig` comando e confirme que ficou bond0 e interface hello está mostrando como backup. 
 
 >[!NOTE]
      >Aplicativos que usam a rede acelerado devem se comunicar através de saudação *bond0* interface não *eth0*.  nome da interface Olá pode alterar antes de rede acelerado alcança disponibilidade geral.

#### <a name="rhelcentos"></a>RHEL/CentOS

Criando um Red Hat Enterprise Linux ou CentOS 7.3 VM requer alguns extra etapas tooload hello mais recentes drivers necessários para a SR-IOV e hello driver VF (função Virtual) para a placa de rede hello. Olá primeira fase de instruções Olá prepara a uma imagem que pode ser usado toomake um ou mais máquinas virtuais com drivers Olá pré-carregado.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Fase um: preparar uma imagem base do Red Hat Enterprise Linux ou CentOS 7.3. 

1.  Provisione uma VM CentOS 7.3 não SRIOV no Azure

2.  Instale o LIS 4.2.2:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Baixe os arquivos de configuração
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Desprovisione essa VM

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  No portal do Azure, parar essa VM; e ir "Discos" do tooVM, captura o URI do VHD do hello OSDisk. Esse URI contém o nome do VHD da imagem base hello e sua conta de armazenamento. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Fase dois: provisionar novas VMs no Azure

1.  Provisionar novas VMs com base em com New-AzureRMVMConfig usando Olá a imagem base do VHD capturado na fase 1, com AcceleratedNetworking ativado vNIC hello:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Depois de inicializam as VMs, verifique o dispositivo de FV hello, "lspci" e verifique Olá Mellanox entrada. Por exemplo, podemos deve ver este item na saída de lspci Olá:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Execute script de acoplamento Olá por:

    ```bash
    sudo bondvf.sh
    ```

4.  Reinicializar Olá novas VMs:

    ```bash
    sudo reboot
    ```

Olá VM deve começar com bond0 configurado e hello caminho acelerado de rede habilitado.  Executar `ifconfig` tooconfirm.
