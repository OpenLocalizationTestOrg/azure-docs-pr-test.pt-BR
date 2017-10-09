---
title: "as configurações de DNS em um arquivo de configuração do serviço de aaaSpecifying | Microsoft Docs"
description: "especificando as configurações DNS personalizadas usando o arquivo de configuração de serviço para uma rede virtual"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="88659-103">Especificando as configurações de DNS em um arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="88659-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="88659-104">Elementos DNS</span><span class="sxs-lookup"><span data-stu-id="88659-104">DNS elements</span></span>
<span data-ttu-id="88659-105">Um arquivo de configuração de serviço pode conter um elemento DnsServers com uma lista de endereços IPv4 para servidores de sistema de nome de domínio (DNS) de Olá Olá serviço usará.</span><span class="sxs-lookup"><span data-stu-id="88659-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="88659-106">As configurações no arquivo de configuração do serviço de saudação têm precedência sobre configurações no arquivo de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="88659-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="88659-107">Para obter mais informações, consulte [Esquema de configuração de serviço do Azure (arquivo .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="88659-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="88659-108">**Elemento NetworkConfiguration**</span><span class="sxs-lookup"><span data-stu-id="88659-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="88659-109">Olá **nome** atributo Olá **DnsServer** elemento é usado apenas como um nome de referência.</span><span class="sxs-lookup"><span data-stu-id="88659-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="88659-110">Ele não representa o nome do host de saudação para o servidor DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="88659-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="88659-111">Cada **DnsServer** valor do atributo deve ser exclusivo entre a assinatura do Microsoft Azure toda hello.</span><span class="sxs-lookup"><span data-stu-id="88659-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="88659-112">Consulte também</span><span class="sxs-lookup"><span data-stu-id="88659-112">See Also</span></span>
[<span data-ttu-id="88659-113">Esquema de configuração de serviço do Azure (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="88659-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="88659-114">Esquema de configuração de Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="88659-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="88659-115">Configurar uma Rede Virtual usando arquivos de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="88659-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="88659-116">Sobre as configurações de rede Virtual no Portal de gerenciamento de saudação</span><span class="sxs-lookup"><span data-stu-id="88659-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

