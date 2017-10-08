---
title: "Guia de solução de problemas de DNS aaaAzure | Microsoft Docs"
description: Como tootroubleshoot comum problemas de DNS do Azure
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Guia de solução de problemas do DNS do Azure

Esta página fornece informações sobre solução de questões de DNS do Azure.

Se essas etapas não resolverem o problema, você pode também procurar ou poste seu problema no nosso [Fórum de suporte da comunidade no MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). Como alternativa, abra uma solicitação de suporte do Azure.


## <a name="i-cant-create-a-dns-zone"></a>Não consigo criar uma zona DNS

problemas comuns de tooresolve, tente um ou mais dos Olá etapas a seguir:

1.  Olá revisão que auditoria de DNS do Azure registra o motivo da falha toodetermine hello.
2.  Cada nome de zona DNS deve ser exclusivo dentro de seu grupo de recursos. Ou seja, duas zonas DNS com hello mesmo nome não é possível compartilhar um grupo de recursos. Tente usar um nome de zona diferente ou outro grupo de recursos.
3.  Você pode ver um erro "Você atingiu ou excedeu o número máximo de saudação de zonas na assinatura {id da assinatura}." Use uma assinatura do Azure diferente, exclua algumas regiões ou entre em contato com o suporte do Azure tooraise seu limite de assinatura.
4.  Você pode ver um erro "zona Olá '{nome da zona}' não está disponível." Esse erro significa que o DNS do Azure foi tooallocate não é possível de servidores de nome para esta zona DNS. Tente usar um nome de zona diferente. Como alternativa, se você for o proprietário do nome de domínio hello, entre em contato com o suporte do Azure, que pode alocar a servidores de nomes para você.


### <a name="recommended-documents"></a>**Documentos recomendados**

[Zonas e registros DNS](dns-zones-records.md)
<br>
[Criar uma zona DNS](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>Não consigo criar um registro DNS

problemas comuns de tooresolve, tente um ou mais dos Olá etapas a seguir:

1.  Olá revisão que auditoria de DNS do Azure registra o motivo da falha toodetermine hello.
2.  Conjunto de registros de saudação já existe?  DNS do Azure gerencia usando o registro de registros *define*, que são a coleção de saudação dos registros de saudação de mesmo nome e Olá mesmo tipo. Se um registro com hello mesmo nome e tipo já existir, em seguida, tooadd outro registro inexistente Olá existente registro deve ser editado definido.
3.  Você está tentando toocreate um registro no ápice de zona DNS de saudação (raiz da zona Olá Olá)? Se assim, Olá convenção DNS é toouse Olá ' @' caractere como o nome do registro hello. Observe também que os padrões DNS Olá não permitir registros CNAME no ápice da zona de saudação.
4.  Existe um conflito de CNAME?  padrões DNS Olá não permitem um registro CNAME com o mesmo nome como um registro de qualquer outro tipo de saudação. Se você tiver um CNAME existente, criando um registro com hello falha de mesmo nome de um tipo diferente.  Da mesma forma, criar um CNAME falhará se o nome da saudação corresponde a um registro existente de um tipo diferente. Remova conflitos Olá removendo Olá outro registro ou escolha um nome de registro diferente.
5.  Foi atingido o limite Olá número de saudação de conjuntos de registros permitido em uma zona DNS? número atual de saudação do registro define e hello número máximo de conjuntos de registros é mostrado em Olá portal do Azure, em Olá 'Propriedades' para a zona de saudação. Se você atingiu o limite, em seguida, exclua alguns conjuntos de registros ou entre em contato com o suporte do Azure tooraise seu limite de conjunto de registros para esta zona, em seguida, tente novamente. 


### <a name="recommended-documents"></a>**Documentos recomendados**

[Zonas e registros DNS](dns-zones-records.md)
<br>
[Criar uma zona DNS](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>Não consigo resolver meu registro DNS

A resolução de nome DNS é um processo de várias etapas que pode falhar por várias razões. Olá seguinte ajudá-lo a investigar por que a resolução DNS está falhando para um registro DNS em uma zona hospedado no DNS do Azure.

1.  Confirme se os registros DNS Olá foi configurados corretamente no DNS do Azure. Examine os registros DNS Olá no hello portal do Azure, verificando se o nome da zona Olá, nome do registro e tipo de registro estão corretas.
2.  Confirme que os registros DNS Olá resolver corretamente nos servidores de nome DNS do Azure hello.
    - Se você fizer consultas DNS do seu computador local, você poderá ver resultados em cache que não refletem o estado atual de Olá Olá de servidores de nomes.  Além disso, redes corporativas geralmente usam servidores de proxy DNS, que impedirá que as consultas DNS que está sendo direcionado toospecific servidores de nome.  tooavoid esses problemas, use um serviço de resolução de nome baseado na web, como [digwebinterface](http://digwebinterface.com).
    - Ser toospecify-se de que os servidores de nome correto de Olá para a zona DNS, conforme mostrado no hello portal do Azure.
    - Verifique se o nome DNS de saudação está correta (tiver toospecify nome de saudação totalmente qualificada, incluindo o nome da zona Olá) e Olá tipo de registro está correto
3.  Confirmar este nome de domínio DNS Olá foi corretamente [delegado servidores de nome DNS do Azure toohello](dns-domain-delegation.md). Há [vários sites da Web de terceiros que oferecem validação de delegação DNS](https://www.bing.com/search?q=dns+check+tool). Este teste é um *zona* teste de delegação, para que você só deve digitar o nome da zona DNS hello e não Olá nome totalmente qualificado registro.
4.  Tendo concluído Olá acima, o registro de DNS deve agora resolver corretamente. tooverify, você pode usar novamente [digwebinterface](http://digwebinterface.com), desta vez usando as configurações de servidor de nome de padrão hello.


### <a name="recommended-documents"></a>**Documentos recomendados**

[Delegar um tooAzure de domínio DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Como especificar hello 'serviço' e 'protocolo' para um registro SRV?

DNS do Azure gerencia registros DNS como conjuntos de registros — Olá conjunto de registros com hello mesmo nome e Olá mesmo tipo. Para um conjunto de registros SRV, Olá 'serviço' e 'protocolo' necessário toobe especificado como parte do nome do conjunto de registros de saudação. Olá outros SRV ('priority', 'peso', 'porta' e 'target') são especificados separadamente para cada registro no conjunto de registros de saudação.

Exemplo de nomes de registro SRV (nome de serviço 'sip', protocolo 'tcp'):

- \_SIP. \_tcp (cria um registro definida no ápice da zona de saudação)
- \_sip.\_tcp.sipservice (cria um conjunto de registros chamado 'sipservice')

### <a name="recommended-documents"></a>**Documentos recomendados**

[Zonas e registros DNS](dns-zones-records.md)
<br>
[Criar conjuntos de registros de DNS e registros usando Olá portal do Azure](dns-getstarted-create-recordset-portal.md)
<br>
[Tipo de registro SRV (Wikipédia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre [registros e zonas DNS do Azure](dns-zones-records.md)
* toostart usando o DNS do Azure, Aprenda como muito[criar uma zona DNS](dns-getstarted-create-dnszone-portal.md) e [criar registros DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate uma zona DNS existente, saiba como muito[importar e exportar um arquivo de zona DNS](dns-import-export.md).

