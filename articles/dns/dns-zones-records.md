---
title: "aaaDNS zonas e os registros de visão geral – DNS do Azure | Microsoft Docs"
description: "Visão geral do suporte à hospedagem de zonas e registros DNS no DNS do Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>Visão geral de zonas e registros DNS

Esta página explica os principais conceitos de saudação de domínios, zonas DNS e registros de DNS e conjuntos de registros e como eles são suportados no DNS do Azure.

## <a name="domain-names"></a>Nomes de domínio

Olá, sistema de nomes de domínio é uma hierarquia de domínios. hierarquia de saudação começa do domínio de 'root' hello, cujo nome é simplesmente '**.**'.  Abaixo dele vêm domínios de nível superior, como 'com', 'net', 'org', 'uk' ou 'jp'.  Abaixo desses estão domínios de segundo nível, como 'org.uk' ou 'co.jp'. domínios de saudação na hierarquia DNS Olá globalmente são distribuídos, hospedadas por servidores de nome DNS em torno de Olá, mundo.

Um registrador de nome de domínio é uma organização que permite que você toopurchase um nome de domínio, como "contoso.com".  Comprar um domínio oferece nome hello toocontrol direita Olá hierarquia DNS com esse nome, por exemplo, permitindo toodirect nome hello "www.contoso.com" tooyour empresa web site. registrador Olá pode domínio Olá em seus próprios servidores de nome em seu nome de host ou permitir que os servidores de nome alternativo de toospecify.

DNS do Azure fornece uma infraestrutura de servidor de nome globalmente distribuídos, alta disponibilidade, que você pode usar toohost seu domínio. Ao hospedar seus domínios no DNS do Azure, você pode gerenciar seus registros DNS com hello mesmo credenciais, APIs, ferramentas, cobrança e suporte para os outros serviços do Azure.

O DNS do Azure não dá suporte a compra de nomes de domínio. Se você quiser toopurchase um nome de domínio, você precisa toouse um registrador de nomes de domínio de terceiro. registrador Olá normalmente cobra uma pequena taxa anual. domínios Olá, em seguida, podem ser hospedados no Azure DNS para o gerenciamento de registros de DNS. Consulte [delegar tooAzure um domínio DNS](dns-domain-delegation.md) para obter detalhes.

## <a name="dns-zones"></a>Zonas DNS

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>Registros DNS

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Vida útil

tempo de saudação toolive ou TTL, especifica quanto tempo cada registro é armazenado em cache por clientes antes que está sendo consultada novamente. Em Olá exemplo acima, Olá TTL é 3600 segundos ou 1 hora.

No DNS do Azure, Olá TTL é especificado para o conjunto de registros de hello, não para cada registro, portanto Olá mesmo valor é usado para todos os registros no registro definido.  Você pode especificar qualquer valor de TTL entre 1 e 2.147.483.647 segundos.

### <a name="wildcard-records"></a>Registros curinga

O DNS do Azure dá suporte a [registros curinga](https://en.wikipedia.org/wiki/Wildcard_DNS_record). Registros de curinga são retornados na consulta de tooany de resposta com um nome correspondente (a menos que haja uma correspondência mais próxima de um conjunto de registros não curinga). O DNS do Azure dá suporte a conjuntos de registros curinga para todos os tipos de registro, exceto NS e SOA.

toocreate um registro de curinga definido, use o nome do conjunto de registros de saudação '\*'. Como alternativa, você também pode usar um nome com '\*'como seu rótulo na extremidade esquerda, por exemplo,'\*.foo '.

### <a name="cname-records"></a>Registros CNAME

Conjuntos de registros CNAME não podem coexistir com outros conjuntos de registros com hello o mesmo nome. Por exemplo, você não pode criar um registro CNAME com o nome relativo do hello "www" e um um registro com nome relativo hello "www" em Olá mesmo tempo.

Porque ápice da zona de saudação (nome = ' @') sempre contém o registro de NS e SOA Olá conjuntos que foram criados quando a zona de saudação foi criada, você não pode criar um registro CNAME definido no ápice da zona de saudação.

Essas restrições são provenientes de padrões do DNS hello e não são as limitações de DNS do Azure.

### <a name="ns-records"></a>Registros NS

conjunto de registros de saudação NS no ápice da zona de saudação (nome ' @') é criada automaticamente com cada zona DNS e é excluído automaticamente quando Olá zona é excluída (ele não pode ser excluído separadamente).

Este conjunto de registros contém nomes de saudação da zona do hello Azure DNS nome servidores toohello atribuído. Você pode adicionar nome adicionais servidores toothis NS conjunto de registros, toosupport co-hospedagem domínios com mais de um provedor DNS. Você também pode modificar hello TTL e metadados para esse conjunto de registros. No entanto, você não pode remover ou modificar servidores de nome DNS do Azure preenchidos previamente hello. 

Observe que isso se aplica apenas toohello NS conjunto de registros no ápice da zona de saudação. Outros conjuntos de registros NS na zona (como zonas de filho usado toodelegate) podem ser criados, modificados e excluídos sem restrição.

### <a name="soa-records"></a>Registros SOA

Um conjunto de registros SOA é criado automaticamente no ápice da saudação de cada zona (nome = ' @') e é excluído automaticamente quando Olá zona é excluída.  Os registros SOA não podem ser criados ou excluídos separadamente.

Você pode modificar todas as propriedades de registro SOA hello, exceto a propriedade de 'host' hello, que é pré-configurado toorefer toohello primário nome do servidor fornecido pelo DNS do Azure.

### <a name="spf-records"></a>Registros SPF

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>Registros SRV

[Registros SRV](https://en.wikipedia.org/wiki/SRV_record) são usados por vários locais de servidor toospecify de serviços. Ao especificar um registro SRV no DNS do Azure:

* Olá *service* e *protocolo* deve ser especificado como parte do nome do conjunto de registros de hello, prefixado com sublinhados.  Por exemplo, '\_sip.\_tcp.nome'.  Para um registro no ápice da zona de Olá, não há nenhuma necessidade toospecify ' @' no nome do registro hello, basta usar Olá serviço e o protocolo, por exemplo '\_sip.\_ TCP'.
* Olá *prioridade*, *peso*, *porta*, e *destino* são especificados como parâmetros de cada registro no conjunto de registros de saudação.

### <a name="txt-records"></a>Registros TXT

Registros TXT são usados toomap nomes de domínio tooarbitrary caracteres de texto. Eles são usados em vários aplicativos, configuração de tooemail relacionados em particular, como Olá [remetente política Framework (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) e [DomainKeys identificado Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).

padrões DNS Olá permitem que um único toocontain de registro TXT várias cadeias de caracteres, cada um deles pode ser too254 caracteres de comprimento. Quando várias cadeias de caracteres são usadas, elas são concatenadas pelos clientes e tratadas como uma única cadeia de caracteres.

Ao chamar hello API de REST do DNS do Azure, é necessário toospecify cada cadeia de caracteres TXT separadamente.  Ao usar o hello portal do Azure, PowerShell ou CLI interfaces você deve especificar uma única cadeia de caracteres por registro, que automaticamente é dividido em segmentos de 254 caracteres, se necessário.

Olá várias cadeias de caracteres em um registro DNS não devem ser confundidas com hello vários registros TXT em um conjunto de registros TXT.  Um conjunto de registros TXT pode conter vários registros e *cada um deles* pode conter várias cadeias de caracteres.  DNS do Azure oferece suporte a um comprimento de cadeia de caracteres total de caracteres too1024 em cada registro TXT definido (entre todos os registros combinados).

## <a name="tags-and-metadata"></a>Marcas e metadados

### <a name="tags"></a>Marcas

Marcas são uma lista de pares nome-valor e são usadas pelo Gerenciador de recursos do Azure toolabel recursos.  Gerenciador de recursos do Azure usa marcas tooenable filtrado exibições de sua conta do Azure e também permite que você tooset uma política na qual as marcas são necessários. Para obter mais informações sobre marcas, consulte [usando marcas tooorganize seus recursos do Azure](../azure-resource-manager/resource-group-using-tags.md).

O DNS do Azure dá suporte ao uso de marcas do Azure Resource Manager em recursos de zona DNS.  Ele não oferece suporte a marcas em conjuntos de registros DNS, embora "metadados" tenham suporte nos Conjuntos de registros DNS como uma alternativa, conforme explicado abaixo.

### <a name="metadata"></a>Metadados

Como uma alternativa toorecord definir marcas, DNS do Azure oferece suporte anotando conjuntos de registros usando 'metadata'.  Tootags semelhante, metadados permitem que você tooassociate pares nome-valor com cada conjunto de registros.  Isso pode ser útil, por exemplo toorecord finalidade de saudação de cada registro definido.  Ao contrário das marcas, os metadados não podem ser usado tooprovide uma exibição filtrada de sua conta do Azure e não podem ser especificado em uma política do Gerenciador de recursos do Azure.

## <a name="etags"></a>ETags

Suponha que duas pessoas ou dois processos tente toomodify um registro DNS no hello mesmo tempo. Qual vence? E o vencedor Olá saber o que eles já substituído alterações criadas por outra pessoa?

DNS do Azure usa Etags toohandle alterações simultâneas toohello mesmo recurso com segurança. As Etags são separadas das ["Marcações" do Azure Resource Manager](#tags). Cada recurso DNS (zona ou conjunto de registros) tem uma Etag associada a ele. Sempre que um recurso é recuperado, a Etag também é recuperada. Ao atualizar um recurso, você pode escolher fazer toopass Olá Etag para verificar que Olá Etag no hello coincide com o servidor DNS do Azure. Como cada recurso de tooa atualização resulta em Olá Etag geradas novamente, uma incompatibilidade de Etag indica que ocorreu uma alteração simultânea. ETags também pode ser usadas ao criar um novo tooensure de recurso que recursos Olá já não existe.

Por padrão, o DNS do Azure PowerShell usa Etags tooblock alterações simultâneas toozones e conjuntos de registros. Olá opcional *-substituir* switch pode ser usado toosuppress verificações de Etag, caso em que qualquer simultâneas alterações que ocorreram são substituídas.

No nível de saudação do hello API de REST do DNS do Azure, Etags são especificadas usando cabeçalhos HTTP.  Seu comportamento é determinado em Olá a tabela a seguir:

| Cabeçalho | Comportamento |
| --- | --- |
| Nenhum |PUT sempre terá êxito (nenhuma verificação de Etag) |
| If-match <etag> |PUT só terá êxito se o recurso existir e a Etag corresponder |
| If-match * |PUT só terá êxito se houver recursos |
| If-none-match * |PUT só terá êxito se não houver recursos |


## <a name="limits"></a>limites

Olá limites padrão a seguir se aplicam ao usar o DNS do Azure:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>Próximas etapas

* toostart usando o DNS do Azure, Aprenda como muito[criar uma zona DNS](dns-getstarted-create-dnszone-portal.md) e [criar registros DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate uma zona DNS existente, saiba como muito[importar e exportar um arquivo de zona DNS](dns-import-export.md).
