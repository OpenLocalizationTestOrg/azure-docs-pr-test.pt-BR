---
title: aaaOverview de DNS reverso no Azure | Microsoft Docs
description: Saiba como funciona o DNS reverso e como ele pode ser usado no Azure
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Visão geral de DNS reverso e suporte no Azure

Este artigo fornece uma visão geral de como inversa DNS funciona e hello cenários inversas de DNS com suporte no Azure.

## <a name="what-is-reverse-dns"></a>O que é DNS reverso?

Os registros DNS convencionais habilitar um mapeamento de um endereço IP do DNS nome (como "www.contoso.com") tooan (como 64.4.6.100).  Reversa de DNS permite que a tradução de saudação de um nome de tooa back (64.4.6.100) do endereço IP ("www.contoso.com").

Registros DNS reversos são usados em uma variedade de situações. Por exemplo, registros DNS reversos são amplamente usados no combate spam de email, verificando o remetente de saudação de uma mensagem de email.  recupera de servidor de email recebimento Olá Olá registro DNS reverso de enviar o endereço IP do servidor de saudação e verifica se que hospedam email toosend autorizados Olá originária domínio. 

## <a name="how-reverse-dns-works"></a>Como funciona o DNS reverso

Os registros do DNS reverso são hospedados em zonas DNS especiais, conhecidas como zonas 'ARPA'.  Essas zonas formam uma hierarquia DNS separada em paralelo com a hierarquia de normal Olá hospedagem domínios como 'contoso.com'.

Por exemplo, Olá 'www.contoso.com' do registro de DNS é implementado usando um registro DNS 'A' com nome hello www na zona de saudação 'contoso.com'.  Esse registro pontos toohello correspondente o endereço IP, neste caso 64.4.6.100.  pesquisa inversa Olá é implementada separadamente, usando um registro de 'PTR' denominado '100' na zona de saudação '6.4.64.in-addr.arpa' (Observe que os endereços IP são revertidos em zonas ARPA.)  Esse registro PTR, se ele tiver sido configurado corretamente, pontos de nome toohello 'www.contoso.com'.

Quando uma organização recebe um bloco de endereço IP, eles também adquirem zona Olá ARPA correspondente à direita toomanage hello. Olá zonas ARPA correspondente endereço IP toohello blocos usados pelo Azure hospedados e gerenciados pela Microsoft. Seu ISP pode hospedar a zona ARPA Olá para seus próprios endereços IP para você, ou pode permitir tooyou host zona ARPA Olá em um serviço DNS de sua escolha, como DNS do Azure.

> [!NOTE]
> As pesquisas DNS diretas e as pesquisas DNS inversas são implementadas em hierarquias de DNS separadas e paralelas. saudação de pesquisa inversa de 'www.contoso.com' é **não** hospedado na zona hello "contoso.com", em vez disso, ele está hospedado na zona ARPA Olá para o bloco de endereço IP correspondente hello. Zonas separadas são usadas para blocos de endereço IPv4 e IPv6.

### <a name="ipv4"></a>IPv4

nome de saudação de uma zona de pesquisa inversa IPv4 deve estar no hello formato a seguir: `<IPv4 network prefix in reverse order>.in-addr.arpa`.

Por exemplo, ao criar uma zona inversa toohost registros para hosts com IPs que estão no prefixo de 192.0.2.0/24 Olá, nome da zona Olá seria criado isolando o prefixo de rede de saudação do endereço da saudação (192.0.2) e invertendo a ordem da saudação (2.0.192) e adicionando Olá sufixo `.in-addr.arpa`.

|Classe de sub-rede|Prefixo de rede  |Prefixo de rede invertido  |Sufixo padrão  |Nome da zona inversa |
|-------|----------------|------------|-----------------|---------------------------|
|Classe A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|Classe B|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|Classe C|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>Delegação de IPv4 sem classe

Em alguns casos, o intervalo IP de saudação alocado tooan organização é menor do que uma classe C (/ 24) intervalo. Nesse caso, o intervalo de IP hello não está em um limite de zona em Olá `.in-addr.arpa` hierarquia da zona e, portanto, não pode ser delegada como uma zona filho.

Em vez disso, um mecanismo diferente é usado tooa dedicado zona DNS de registros de controle de tootransfer de pesquisa inversa individual (PTR). Esse mecanismo delega uma zona filho para cada intervalo IP e mapeia cada endereço IP no hello individualmente intervalo toothat zona de filho usando registros CNAME.

Por exemplo, suponha que uma organização recebe Olá IP intervalo 192.0.2.128/26 por seu ISP. Isso representa 64 endereços IP, de 192.0.2.128 too192.0.2.191. O DNS reverso para esse intervalo é implementado da seguinte maneira:
- organização de saudação cria uma zona de pesquisa inversa chamada 128-26.2.0.192.in-addr. arpa. prefixo de saudação ' 128-26' representa Olá rede segmento atribuído toohello organização dentro Olá classe C (/ 24) intervalo.
- Olá ISP cria tooset de registros NS backup Olá delegação de saudação acima da zona DNS da zona de pai de classe C hello. Ele também cria registros CNAME na zona de pesquisa inversa do hello pai (classe C), cada endereço IP na Olá IP intervalo toohello nova zona criada pela organização de saudação de mapeamento:

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- Olá organização e gerencia os registros PTR individuais hello dentro de suas zonas filho.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Uma pesquisa inversa para consultas de endereço '192.0.2.129' hello IP para um registro PTR chamado '129.2.0.192.in-addr.arpa'. Essa consulta resolve via Olá CNAME no registro PTR Olá pai zona toohello na zona de filho hello.

### <a name="ipv6"></a>IPv6

nome de saudação de uma zona de pesquisa inversa IPv6 deve estar no hello formulário a seguir:`<IPv6 network prefix in reverse order>.ip6.arpa`

Por exemplo, Ao criar uma zona inversa toohost registros para hosts com IPs que estão em Olá 2001:db8:1000:abdc:: / 64 prefixo, nome da zona Olá seria criado isolando o prefixo de rede de saudação do endereço da saudação (2001:db8:abdc::). Em seguida, expanda tooremove de prefixo de rede IPv6 de saudação [zero compactação](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), se ele foi o prefixo de endereço usado tooshorten Olá IPv6 (2001:0db8:abdc:0000::). Olá ordem inversa, usando um período como Olá delimitador entre cada número hexadecimal no prefixo hello, Olá toobuild revertida prefixo de rede (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) e adicione o sufixo Olá `.ip6.arpa`.


|Prefixo de rede  |Prefixo de rede expandido e invertido |Sufixo padrão |Nome da zona inversa  |
|---------|---------|---------|---------|
|2001:db8:abdc::/64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | .ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102::/64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | .ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Suporte do Azure para DNS reverso

Azure oferece suporte a dois cenários separados relacionadas tooreverse DNS:

**Olá pesquisa inversa zona correspondente tooyour bloco de endereço IP de hospedagem.**
DNS do Azure podem ser usados de maneira muito[hospedar as zonas de pesquisa inversa e gerenciar registros PTR Olá para cada pesquisa inversa de DNS](dns-reverse-dns-hosting.md), tanto para IPv4 quanto IPv6.  Olá o processo de criação de zona de pesquisa inversa (ARPA) Olá, configurar a delegação de saudação e configurando PTR registros é Olá mesmo que para as zonas DNS regulares.  Olá apenas as diferenças são que Olá delegação deve ser configurada por meio de seu ISP, em vez de um registrador de DNS e Olá tipo de registro PTR deve ser usado.

**Configure o registro DNS reverso Olá para o endereço IP hello atribuído tooyour serviço do Azure.** Azure permite muito[Configurar pesquisa inversa Olá para endereços IP de saudação alocados tooyour serviço do Azure](dns-reverse-dns-for-azure-services.md).  Esta pesquisa inversa é configurada pelo Azure como um registro PTR na zona ARPA correspondente hello.  Essas zonas ARPA, correspondente a intervalos IP hello tooall usados pelo Azure, hospedadas pela Microsoft

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre DNS reverso, confira [Pesquisa de DNS reverso na Wikipédia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Saiba como muito[zona de pesquisa inversa de saudação de host para o intervalo IP atribuído pelo ISP no DNS do Azure](dns-reverse-dns-for-azure-services.md).
<br>
Saiba como muito[gerenciar registros DNS reversos para os serviços do Azure](dns-reverse-dns-for-azure-services.md).

