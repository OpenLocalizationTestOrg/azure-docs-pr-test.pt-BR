---
title: "Visão geral da delegação DNS aaaAzure | Microsoft Docs"
description: "Entenda como usar DNS do Azure e delegação de domínio de toochange nome servidores tooprovide domínio hospedando."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Delegação de zonas DNS com o DNS do Azure

DNS do Azure permite que você toohost uma zona DNS e gerenciar registros DNS Olá para um domínio no Azure. Para consultas DNS para um tooreach de domínio DNS do Azure, domínio Olá tem toobe delegadas tooAzure DNS do domínio pai de saudação. Tenha em mente DNS do Azure não é um registrador de domínio hello. Este artigo explica como funciona a delegação de domínio e domínios de toodelegate tooAzure DNS.

## <a name="how-dns-delegation-works"></a>Como funciona a delegação de DNS

### <a name="domains-and-zones"></a>Zonas e domínios

Olá, sistema de nomes de domínio é uma hierarquia de domínios. hierarquia de saudação começa do domínio de 'root' hello, cujo nome é simplesmente '**.**'.  Abaixo dele vêm domínios de nível superior, como 'com', 'net', 'org', 'uk' ou 'jp'.  Abaixo desses domínios de alto nível estão domínios de segundo nível, como 'org.uk' ou 'co.jp'.  E assim por diante. domínios Olá Olá hierarquia DNS são hospedados usando zonas DNS separadas. Essas zonas são distribuídas globalmente, hospedadas por servidores de nome DNS em torno de Olá, mundo.

**Zona DNS** -um domínio é um nome exclusivo no hello sistema de nomes de domínio, por exemplo 'contoso.com'. Uma zona DNS é usado toohost Olá registros DNS para um domínio específico. Por exemplo, domínio Olá 'contoso.com' pode conter vários registros DNS como mail.contoso.com (para um servidor de email) e www.contoso.com (para um site da Web).

**Registrador de domínio** - Um registrador de domínio é uma empresa que pode fornecer nomes de domínio da Internet. Verifique se, o domínio da Internet Olá toouse está disponível e permitem que você toopurchase-lo. Quando o nome de domínio Olá estiver registrado, você é proprietário legal de Olá Olá nome de domínio. Se você já tiver um domínio da Internet, você usará Olá atual toodelegate tooAzure DNS do domínio registrador.

toofind mais informações sobre quem possui um nome de domínio específico ou para obter informações sobre como toobuy um domínio, consulte [gerenciamento de domínio de Internet no AD do Azure](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Resolução e delegação

Existem dois tipos de servidores DNS:

* Um servidor DNS *autoritativo* hospeda zonas DNS. Ele responde a consultas DNS apenas para registros nessas zonas.
* Um servidor DNS *recursivo* não hospeda zonas DNS. Todas as consultas DNS responde chamando dados DNS com autoridade servidores toogather Olá necessárias.

O Azure DNS fornece um serviço DNS autoritativo.  Ele não fornece um serviço DNS recursivo. Serviços de nuvem e VMs no Azure são automaticamente configurado toouse um serviço DNS recursivo que é fornecido separadamente como parte da infraestrutura do Azure. Para obter informações sobre como toochange essas configurações de DNS, consulte [resolução de nomes no Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

Os clientes DNS em PCs ou dispositivos móveis normalmente chama um tooperform de servidor DNS recursivo todas as consultas DNS Olá aplicativos de cliente precisam.

Quando um servidor DNS recursivo recebe uma consulta para um registro DNS, como "www.contoso.com", ele primeiro precisa toofind Olá nome hospedagem Olá zona do servidor para o domínio de 'contoso.com' hello. servidor de nomes de Olá toofind, ele inicia em servidores de nome raiz hello e daí localiza os servidores de nome hello hospeda Olá 'com' zona. Em seguida, consultar Olá 'com' nome servidores toofind Olá nome servidores hospedando a zona de 'contoso.com' hello.  Finalmente, é possível tooquery esses servidores de nome para 'www.contoso.com'.

Esse procedimento é chamado de resolução de nome DNS hello. Estritamente falando, resolução de DNS inclui etapas adicionais, como a seguir CNAMEs, mas que não é importante toounderstanding como funciona a delegação de DNS.

Como uma zona pai '' toohello nome servidores de ponto para uma zona filho? Ele faz isso usando um tipo especial de registro DNS chamado de registro NS (NS significa 'name server', servidor de nomes). Por exemplo, a zona raiz de saudação contém registros NS para 'com' e mostra Olá servidores de nome para a zona de 'com' hello. Por sua vez, zona de 'com' hello contém registros NS para 'contoso.com', que mostra os servidores de nome Olá para a zona de 'contoso.com' hello. Configurar os registros NS Olá para uma zona filho em uma zona pai é chamado de domínio de Olá delegação.

Olá a imagem a seguir mostra um exemplo de consulta DNS. partners.contoso.NET e Olá contoso.net são zonas de DNS do Azure.

![Servidor de nomes DNS](./media/dns-domain-delegation/image1.png)

1. Olá solicitações de cliente `www.partners.contoso.net` de seu servidor DNS local.
1. servidor DNS local Olá não tem registro de saudação faz uma solicitação ao servidor nome tootheir raiz.
1. servidor de nome Hello raiz não tem registro de saudação, mas sabe o endereço de saudação do hello `.net` servidor de nome, ele fornece esse servidor DNS do endereço toohello
1. Olá DNS envia Olá solicitação toohello `.net` name Server, servidor não tem registro Olá mas não sabe o endereço de saudação do servidor de nomes de contoso.net Olá. Nesse caso é uma zona DNS hospedada no DNS do Azure.
1. zona de saudação `contoso.net` não tem registro de saudação mas sabe o nome do servidor Olá para `partners.contoso.net` e responde com isso. Nesse caso é uma zona DNS hospedada no DNS do Azure.
1. servidor DNS Olá solicita o endereço IP de saudação do `partners.contoso.net` de saudação `partners.contoso.net` zona. Ele contém o registro hello e responde com o endereço IP de saudação.
1. servidor DNS Olá fornece cliente de toohello de endereço IP Olá
1. cliente Olá conecta site toohello `www.partners.contoso.net`.

Cada delegação realmente tem duas cópias dos registros de NS Olá; uma na zona pai de saudação apontando toohello filho e outro na zona de filho Olá em si. zona de 'contoso.net' Hello contém registros de saudação NS para 'contoso.net' (em registros de NS adição toohello em 'net'). Esses registros são chamados os registros NS autoritativos e eles ficam no ápice da saudação da zona de filho hello.

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[delegar tooAzure seu domínio DNS](dns-delegate-domain-azure-dns.md)

