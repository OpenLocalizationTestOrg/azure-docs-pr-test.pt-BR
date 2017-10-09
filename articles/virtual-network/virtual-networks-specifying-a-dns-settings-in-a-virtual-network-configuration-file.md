---
title: "aaaSpecifying as configurações de DNS em um arquivo de configuração de rede virtual | Microsoft Docs"
description: "Como configurações do servidor DNS toochange em uma rede virtual usando uma configuração de rede virtual do arquivo no modelo de implantação clássico Olá"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="20e55-103">Especificando as configurações de DNS em um arquivo de configuração de rede virtual</span><span class="sxs-lookup"><span data-stu-id="20e55-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="20e55-104">Um arquivo de configuração de rede tem dois elementos que você pode usar as configurações do sistema de nome de domínio (DNS) toospecify: **DnsServers** e **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="20e55-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="20e55-105">Você pode adicionar uma lista de servidores DNS especificando seus endereços IP e fazer referência a nomes toohello **DnsServers** elemento.</span><span class="sxs-lookup"><span data-stu-id="20e55-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="20e55-106">Você pode usar um **DnsServerRef** toospecify elemento quais entradas de elemento DnsServers de saudação do servidor DNS são usadas para sites de rede diferente dentro de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="20e55-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="20e55-107">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="20e55-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="20e55-108">arquivo de configuração de rede Olá pode conter Olá elementos a seguir.</span><span class="sxs-lookup"><span data-stu-id="20e55-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="20e55-109">título de saudação de cada elemento é vinculado tooa página que fornece informações adicionais sobre o elemento de saudação configurações do valor.</span><span class="sxs-lookup"><span data-stu-id="20e55-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20e55-110">Para obter informações sobre como tooconfigure Olá arquivo de configuração de rede, consulte [configurar uma rede Virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="20e55-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="20e55-111">Para obter informações sobre cada elemento contido no arquivo de configuração de rede hello, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="20e55-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="20e55-112">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="20e55-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="20e55-113">Olá **nome** atributo Olá **DnsServer** elemento é usado apenas como uma referência para Olá **DnsServerRef** elemento.</span><span class="sxs-lookup"><span data-stu-id="20e55-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="20e55-114">Ele não representa o nome do host de saudação para o servidor DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="20e55-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="20e55-115">Cada **DnsServer** o valor do atributo deve ser exclusivo entre a assinatura do Microsoft Azure toda Olá</span><span class="sxs-lookup"><span data-stu-id="20e55-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="20e55-116">Elemento de Sites de Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="20e55-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="20e55-117">Em ordem toospecify essa configuração para o elemento de Sites de rede Virtual hello, ele deverá ser definido anteriormente no elemento DNS hello.</span><span class="sxs-lookup"><span data-stu-id="20e55-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="20e55-118">Olá DnsServerRef *nome* em Olá Sites de rede Virtual elemento deve se referir a tooa nome valor especificado no elemento DNS Olá para DnsServer *nome*.</span><span class="sxs-lookup"><span data-stu-id="20e55-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="20e55-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20e55-119">Next steps</span></span>
* <span data-ttu-id="20e55-120">Entender Olá [esquema de configuração de rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="20e55-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="20e55-121">Entender Olá [esquema de configuração de serviço do Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="20e55-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="20e55-122">[Configure uma rede virtual usando os arquivos de configuração de Rede](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="20e55-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

