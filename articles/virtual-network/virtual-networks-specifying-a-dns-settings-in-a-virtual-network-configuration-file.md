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
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Especificando as configurações de DNS em um arquivo de configuração de rede virtual
Um arquivo de configuração de rede tem dois elementos que você pode usar as configurações do sistema de nome de domínio (DNS) toospecify: **DnsServers** e **DnsServerRef**. Você pode adicionar uma lista de servidores DNS especificando seus endereços IP e fazer referência a nomes toohello **DnsServers** elemento. Você pode usar um **DnsServerRef** toospecify elemento quais entradas de elemento DnsServers de saudação do servidor DNS são usadas para sites de rede diferente dentro de sua rede virtual.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação clássico hello.

arquivo de configuração de rede Olá pode conter Olá elementos a seguir. título de saudação de cada elemento é vinculado tooa página que fornece informações adicionais sobre o elemento de saudação configurações do valor.

> [!IMPORTANT]
> Para obter informações sobre como tooconfigure Olá arquivo de configuração de rede, consulte [configurar uma rede Virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md). Para obter informações sobre cada elemento contido no arquivo de configuração de rede hello, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[Elemento DNS](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Olá **nome** atributo Olá **DnsServer** elemento é usado apenas como uma referência para Olá **DnsServerRef** elemento. Ele não representa o nome do host de saudação para o servidor DNS de saudação. Cada **DnsServer** o valor do atributo deve ser exclusivo entre a assinatura do Microsoft Azure toda Olá
> 
> 

[Elemento de Sites de Rede Virtual](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> Em ordem toospecify essa configuração para o elemento de Sites de rede Virtual hello, ele deverá ser definido anteriormente no elemento DNS hello. Olá DnsServerRef *nome* em Olá Sites de rede Virtual elemento deve se referir a tooa nome valor especificado no elemento DNS Olá para DnsServer *nome*.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Entender Olá [esquema de configuração de rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093).
* Entender Olá [esquema de configuração de serviço do Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Configure uma rede virtual usando os arquivos de configuração de Rede](virtual-networks-using-network-configuration-file.md).

