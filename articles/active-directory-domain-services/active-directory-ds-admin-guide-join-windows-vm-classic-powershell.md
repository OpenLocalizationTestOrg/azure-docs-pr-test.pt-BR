---
title: "Azure Active Directory Domain Services: guia de administração | Microsoft Docs"
description: "Ingresse em um máquina virtual tooa gerenciado domínio do Windows PowerShell do Azure e o modelo de implantação clássico hello."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>Ingressar em um domínio do Windows Server máquina virtual tooa gerenciado usando o PowerShell
> [!div class="op_single_selector"]
> * [Portal clássico do Azure - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. Serviços de domínio do AD do Azure atualmente não dá suporte para modelo do Gerenciador de recursos de saudação.
>
>

Estas etapas mostram como os comandos toocustomize um conjunto de PowerShell do Azure que criar e pré-configurar a uma máquina virtual baseados no Windows Azure usando uma abordagem de bloco de construção. Essas etapas ajudam a criar uma máquina virtual baseados no Windows Azure e associá-la tooan domínio gerenciado por serviços de domínio do AD do Azure.

Estas etapas seguem uma abordagem de preencher lacunas para criar conjuntos de comandos do Azure PowerShell. Essa abordagem pode ser útil se você for novo tooPowerShell ou deseja tooknow toospecify quais valores de configuração com êxito. Usuários avançados do PowerShell podem executar comandos hello e substitua seus próprios valores para variáveis de saudação (linhas de saudação que começam com "$").

Se você ainda não tiver feito isso, use as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell no computador local. Em seguida, abra um prompt de comando do Windows PowerShell.

## <a name="step-1-add-your-account"></a>Etapa 1: adicionar sua conta
1. No prompt do PowerShell hello, digite **Add-AzureAccount** e clique em **Enter**.
2. Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**.
3. Digite a senha Olá para sua conta.
4. Clique em **Entrar**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Etapa 2: Definir a assinatura e a conta de armazenamento
Defina a assinatura do Azure e a conta de armazenamento executando esses comandos no prompt de comando do Windows PowerShell hello. Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com nomes de saudação correto.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Você pode obter o nome de assinatura correta de saudação do hello propriedade de nome de inscrição da saída de saudação do hello **Get-AzureSubscription** comando. Você pode obter o nome de conta de armazenamento correta de saudação do Olá propriedade do rótulo de saída Olá Olá **Get-AzureStorageAccount** comando depois de executar Olá **Select-AzureSubscription** comando.

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>Etapa 3: Passo a passo - provisionar a máquina virtual de saudação e ingressar em domínio gerenciado toohello
Aqui está Olá correspondente do Azure PowerShell comando conjunto toocreate esta máquina virtual, com linhas em branco entre cada bloco para facilitar a leitura.

Especifique informações sobre toobe de máquina virtual do Windows hello provisionado.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

Para obter valores de InstanceSize Olá para D, DS ou máquinas virtuais de série G, consulte [Máquina Virtual e tamanhos de serviço de nuvem para Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Fornece informações sobre o domínio gerenciado hello.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Especifique o nome de Olá Olá do serviço de nuvem.

    $svcname="Contoso100-test"

Especifique o nome de saudação do Olá Olá de toowhich de rede virtual que VM deve ser unida. Certifique-se de domínio gerenciados AAD-DS Olá está disponível na rede virtual.

    $vnetname="MyPreviewVnet"

Selecione Olá VM imagem toobe usada tooprovision Olá VM.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Configurar Olá VM - nome do conjunto de VM, instância de tamanho e imagem toobe usada.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Obter credenciais de administrador local para Olá VM. Escolha uma senha de administrador local forte.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Obter credenciais para uma conta de usuário que pertencem a domínio grupo de toojoin VM toohello gerenciado administradores too'AAD DC. Não especifique nome de domínio Olá - para instância, em nosso exemplo, podemos especificar 'bob' como nome de usuário de saudação.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Configurar Olá VM - especificar o requisito de associação de domínio e as credenciais necessárias.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Defina uma sub-rede para Olá VM.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

Opcional: Ponto toohello o endereço IP do domínio hello. Se você definir endereços IP de saudação de saudação do hello serviços de domínio do AD do Azure domínio gerenciado toobe servidores DNS da rede virtual Olá, esta etapa não será necessária.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

Agora, Olá provisionar domínio VM do Windows.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Script tooprovision uma VM do Windows e unir automaticamente tooan domínio gerenciado por serviços de domínio do AAD
Esse conjunto de comandos do PowerShell cria uma máquina virtual para um servidor de linha de negócios que:

* Usa a imagem do Windows Server 2012 R2 Datacenter hello.
* É uma máquina virtual extra pequena.
* Tem o nome de saudação Contoso100 teste.
* É automaticamente domínio unidas toohello contoso100 domínio gerenciado.
* É adicionado toohello mesma rede virtual Olá gerenciados domínio.

Aqui está o hello máquina de virtual do Windows hello amostra completa script toocreate e unir automaticamente toohello domínio gerenciado por serviços de domínio do AD do Azure.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
