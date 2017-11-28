---
title: "Especificando as configurações DNS em um arquivo de configuração de Rede Virtual | Microsoft Docs"
description: "Como alterar as configurações do servidor DNS em uma rede virtual usando um arquivo de configuração de rede virtual no modelo de implantação clássica"
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
ms.openlocfilehash: ec33268915a1888509834ce6a5b2bc782a12ce4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="f4fa8-103">Especificando as configurações de DNS em um arquivo de configuração de rede virtual</span><span class="sxs-lookup"><span data-stu-id="f4fa8-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="f4fa8-104">Um arquivo de configuração de rede tem dois elementos que você pode usar para especificar as configurações do Sistema de Nome de Domínio (DNS): **DnsServers** e **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-104">A network configuration file has two elements that you can use to specify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="f4fa8-105">Você pode adicionar uma lista de servidores DNS especificando seus endereços IP e fazendo referência a nomes para o elemento **DnsServers** .</span><span class="sxs-lookup"><span data-stu-id="f4fa8-105">You can add a list of DNS servers by specifying their IP addresses and reference names to the **DnsServers** element.</span></span> <span data-ttu-id="f4fa8-106">Você pode usar um elemento **DnsServerRef** para especificar quais entradas do servidor DNS do elemento DnsServers serão usadas para sites de rede diferentes dentro da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-106">You can then use a **DnsServerRef** element to specify which DNS server entries from the DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f4fa8-107">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-107">This article covers the classic deployment model.</span></span>

<span data-ttu-id="f4fa8-108">O arquivo de configuração de rede pode conter os seguintes elementos.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-108">The network configuration file may contain the following elements.</span></span> <span data-ttu-id="f4fa8-109">O título de cada elemento é vinculado a uma página que fornece informações adicionais sobre as configurações de valores de elemento.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-109">The title of each element is linked to a page that provides additional information about the element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4fa8-110">Para obter informações sobre como configurar o arquivo de configuração de rede, consulte [Configurar uma rede virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="f4fa8-110">For information about how to configure the network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="f4fa8-111">Para obter informações sobre cada elemento contido no arquivo de configuração de rede, consulte [Esquema de configuração de Rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4fa8-111">For information about each element contained in the network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="f4fa8-112">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="f4fa8-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="f4fa8-113">O atributo **nome** no elemento **DnsServer** é usado apenas como uma referência para o elemento**DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-113">The **name** attribute in the **DnsServer** element is used only as a reference for the **DnsServerRef** element.</span></span> <span data-ttu-id="f4fa8-114">Ele não representa o nome do host para o servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-114">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="f4fa8-115">Cada valor do atributo **DnsServer** deve ser exclusivo a toda a assinatura do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f4fa8-115">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="f4fa8-116">Elemento de Sites de Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="f4fa8-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="f4fa8-117">Para especificar esta configuração para o elemento de Sites de Rede Virtual, ela deve ser anteriormente definida no elemento de DNS.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-117">In order to specify this setting for the Virtual Network Sites element, it must be previously defined in the DNS element.</span></span> <span data-ttu-id="f4fa8-118">O *nome* DnsServerRef no elemento Sites de Rede Virtual deve se referir a um valor de nome especificado no elemento de DNS para o *nome* DnsServer.</span><span class="sxs-lookup"><span data-stu-id="f4fa8-118">The DnsServerRef *name* in the Virtual Network Sites element must refer to a name value specified in the DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f4fa8-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4fa8-119">Next steps</span></span>
* <span data-ttu-id="f4fa8-120">Entenda o [Esquema de configuração da Rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="f4fa8-120">Understand the [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="f4fa8-121">Entenda o [Esquema de configuração do Serviço do Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="f4fa8-121">Understand the [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="f4fa8-122">[Configure uma rede virtual usando os arquivos de configuração de Rede](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="f4fa8-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

