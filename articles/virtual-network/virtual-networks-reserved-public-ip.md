---
title: "aaaManage Azure reservado de endereços IP (clássico) - PowerShell | Microsoft Docs"
description: "Entender os endereços IP reservados (clássico) e como toomanage-los usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Endereços IP reservados (Clássico)

> [!div class="op_single_selector"]
> * [portal do Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI do Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modelo](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Clássico)](virtual-networks-reserved-public-ip.md)

Os endereços IP no Azure recaem em duas categorias: dinâmicos e reservados. Os endereços IP públicos gerenciados pelo Azure são dinâmicos por padrão. Que significa que Olá endereço IP usado para um determinado serviço de nuvem (VIP) ou tooaccess uma VM ou instância de função diretamente (ILPIP) pode mudar de tootime de tempo, quando os recursos são desligados ou parados (desalocados).

endereços IP tooprevent alterem, você poderá reservar um endereço IP. IPs reservados podem ser usados apenas como um VIP, garantindo o endereço IP Olá para o serviço de nuvem Olá permanece Olá iguais, mesmo que os recursos foram desligados ou parada (desalocada). Além disso, você pode converter existente IPs dinâmico usado como um endereço IP VIP tooa reservado.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como tooreserve uma estática pública endereço IP usando Olá [modelo de implantação do Gerenciador de recursos](virtual-network-ip-addresses-overview-arm.md).

toolearn mais sobre IP endereços no Azure, leia Olá [endereços IP](virtual-network-ip-addresses-overview-classic.md) artigo.

## <a name="when-do-i-need-a-reserved-ip"></a>Quando eu precisarei de um IP reservado?
* **Você deseja tooensure que Olá IP é reservado em sua assinatura**. Se você quiser tooreserve um endereço IP que não é liberado da sua assinatura sob nenhuma circunstância, você deve usar um IP público reservado.  
* **Você deseja que sua toostay IP com o serviço de nuvem mesmo em interrompido ou desalocadas estado (VMs)**. Se você quiser que seu toobe serviço acessado usando um endereço IP que não são alterados, mesmo quando a nuvem de máquinas virtuais em Olá serviço foram desligados ou parar (desalocado).
* **Você deseja que o tráfego de saída do Azure usa um endereço IP previsível de tooensure**. Você pode ter seu local firewall configurado tooallow somente do tráfego de endereços IP específicos. Ao reservar um IP, você sabe que o IP de origem Olá endereço e não é necessário tooupdate devido a alterações IP tooan de regras de firewall.

## <a name="faq"></a>Perguntas frequentes
1. Posso usar um IP reservado para todos os serviços do Azure? <br>
    Não. Os IPs reservados só podem ser usados para VMs e funções de instância de serviço de nuvem exposto através de um VIP.
2. Quantos IPs reservados eu posso ter? <br>
    Para obter detalhes, consulte Olá [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.
3. Há uma cobrança para IPs reservados? <br>
    Às vezes. Para obter detalhes sobre preços, consulte Olá [detalhes de preço do endereço de IP reservado](http://go.microsoft.com/fwlink/?LinkID=398482) página.
4. Como eu reservo um endereço IP? <br>
    Você pode usar o PowerShell, hello [API de REST de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), ou hello [portal do Azure](https://portal.azure.com) tooreserve um endereço IP em uma região do Azure. Um endereço IP reservado é assinatura tooyour associado.
5. Posso usar um IP reservado com VNets baseadas em grupos de afinidades? <br>
    Não. Os IPs reservados têm suporte apenas em redes virtuais regionais. VNets associadas a grupos de afinidades não dão suporte a IPs reservados. Para obter mais informações sobre como associar uma rede virtual uma região ou grupo de afinidade, consulte Olá [sobre VNets regionais e grupos de afinidade](virtual-networks-migrate-to-regional-vnet.md) artigo.

## <a name="manage-reserved-vips"></a>Gerenciar VIPs reservados

Certifique-se de ter instalado e configurado o PowerShell executando etapas Olá Olá [instalar e configurar o PowerShell](/powershell/azure/overview) artigo. 

Antes de usar IPs reservados, você deve adicionar assinatura tooyour. toocreate um IP reservado no pool de saudação do IP público de endereços disponíveis no hello *centro dos EUA* local, execute Olá comando a seguir:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

Observe, entretanto, que você não pode especificar qual IP está sendo reservado. tooview quais endereços IP estão reservados em sua assinatura, execute Olá a seguir de comando do PowerShell e observe valores hello *ReservedIPName* e *endereço*:

```powershell
Get-AzureReservedIP
```

Saída esperada:

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>Quando você cria um endereço IP reservado com o PowerShell, você não pode especificar um IP de Olá reservada do recurso grupo toocreate no. O Azure o coloca automaticamente em um grupo de recursos denominado *Default-Networking*. Se você criar o IP reservada de saudação usando Olá [portal do Azure](http://portal.azure.com), você pode especificar qualquer grupo de recursos que você escolher. Se você criar IP hello reservado em um grupo de recursos diferente de *rede padrão* no entanto, sempre que referenciar Olá IP reservado com comandos como `Get-AzureReservedIP` e `Remove-AzureReservedIP`, você deve fazer referência a nome hello *Reservado-ip-nome de nome do grupo de recursos do grupo*.  Por exemplo, se você criar um IP reservado denominado *myReservedIP* em um grupo de recursos denominado *myResourceGroup*, você deve fazer referência a nome de saudação do IP hello reservado como *myResourceGroup de grupo myReservedIP*.   

Quando um IP é reservado, ela permanece associada tooyour assinatura até você excluí-lo. toodelete um IP reservado, Olá executar comandos do PowerShell a seguir:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Reservar um endereço IP de saudação de um serviço de nuvem existente
Você pode reservar o endereço IP de saudação de um serviço de nuvem existente adicionando Olá `-ServiceName` parâmetro. endereço IP de saudação tooreserve de um serviço de nuvem *TestService* em Olá *centro dos EUA* local, execute Olá comando PowerShell a seguir:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Associar um reservado IP tooa novo serviço de nuvem
Olá script a seguir cria um IP reservado novo, em seguida, associa-tooa novo serviço de nuvem chamado *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> Quando você cria um toouse IP reservado com um serviço de nuvem, você ainda consultar toohello VM usando *VIP:&lt;número da porta >* para comunicação de entrada. Reservar um IP não significa que você pode conectar toohello VM diretamente. Olá IP reservado é atribuído toohello nuvem de serviço que Olá VM foi implantada. Se você quiser tooconnect tooa VM por IP diretamente, você tem tooconfigure um IP público em nível de instância. Um IP público em nível de instância é um tipo de IP público (chamado de um ILPIP) atribuído diretamente tooyour VM. Ele não pode ser reservado. Para obter mais informações, leia Olá [IP público em nível de instância (ILPIP)](virtual-networks-instance-level-public-ip.md) artigo.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Remover um IP reservado de uma implantação em execução
tooremove um IP reservado adicionado um novo serviço de nuvem tooa, execute o hello comando PowerShell a seguir:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Removendo um IP reservado de uma implantação em execução não remove reserva Olá de sua assinatura. Ele simplesmente libera Olá IP toobe usado por outro recurso em sua assinatura.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Associar um tooa IP reservado executando a implantação
Olá, comandos a seguir criam um serviço de nuvem chamado *TestService2* com uma nova VM denominada *TestVM2*. Olá existente reservado IP denominado *MyReservedIP* é, em seguida, o serviço de nuvem toohello associado.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Associar um serviço de nuvem tooa IP reservado por meio de um arquivo de configuração de serviço
Você também pode associar um serviço de nuvem tooa IP reservado, usando um arquivo de configuração (CSCFG) do serviço. Olá xml de exemplo a seguir mostra como tooconfigure um serviço de nuvem toouse um VIP reservado nomeados *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Próximas etapas
* Entender como [endereçamento IP](virtual-network-ip-addresses-overview-classic.md) funciona no modelo de implantação clássico hello.
* Saiba mais sobre [endereços IP privados reservados](virtual-networks-reserved-private-ip.md).
* Saiba mais sobre [endereços ILPIP (IP Público de Nível de Instância)](virtual-networks-instance-level-public-ip.md).

