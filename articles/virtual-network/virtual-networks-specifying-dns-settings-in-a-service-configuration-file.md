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
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Especificando as configurações de DNS em um arquivo de configuração de serviço
## <a name="dns-elements"></a>Elementos DNS
Um arquivo de configuração de serviço pode conter um elemento DnsServers com uma lista de endereços IPv4 para servidores de sistema de nome de domínio (DNS) de Olá Olá serviço usará. As configurações no arquivo de configuração do serviço de saudação têm precedência sobre configurações no arquivo de configuração de rede hello. Para obter mais informações, consulte [Esquema de configuração de serviço do Azure (arquivo .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Elemento NetworkConfiguration**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Olá **nome** atributo Olá **DnsServer** elemento é usado apenas como um nome de referência. Ele não representa o nome do host de saudação para o servidor DNS de saudação. Cada **DnsServer** valor do atributo deve ser exclusivo entre a assinatura do Microsoft Azure toda hello.
> 
> 

## <a name="see-also"></a>Consulte também
[Esquema de configuração de serviço do Azure (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Esquema de configuração de Rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Configurar uma Rede Virtual usando arquivos de configuração de rede](http://go.microsoft.com/fwlink/?LinkId=248094)

[Sobre as configurações de rede Virtual no Portal de gerenciamento de saudação](http://go.microsoft.com/fwlink/?LinkId=248092)

