---
title: aaaAzure Traffic Manager - perguntas frequentes | Microsoft Docs
description: "Este artigo fornece respostas toofrequently perguntas frequentes sobre o Gerenciador de tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Perguntas frequentes sobre o Gerenciador de Tráfego

## <a name="traffic-manager-basics"></a>Noções básicas sobre o Gerenciador de Tráfego

### <a name="what-ip-address-does-traffic-manager-use"></a>Qual endereço IP o Gerenciador de Tráfego usa?

Conforme explicado em [como o Gerenciador de tráfego funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), o Traffic Manager funciona no nível DNS de saudação. Envia as respostas DNS serviço apropriado do toohello toodirect clientes ponto de extremidade. Clientes, em seguida, conecte-se ponto de extremidade de serviço toohello diretamente, não pelo Gerenciador de tráfego.

Portanto, o Traffic Manager não fornece um ponto de extremidade ou o endereço IP para clientes tooconnect para. Portanto, se você quiser o endereço IP estático para seu serviço, que deve ser configurado no serviço hello, não no Gerenciador de tráfego.

### <a name="does-traffic-manager-support-sticky-sessions"></a>O Gerenciador de Tráfego dá suporte a sessões “temporárias”?

Conforme explicado em [como o Gerenciador de tráfego funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), o Traffic Manager funciona no nível DNS de saudação. Ele usa o DNS respostas toodirect clientes toohello serviço apropriado ponto de extremidade. Os clientes se conectam toohello ponto de extremidade de serviço diretamente, não pelo Gerenciador de tráfego. Portanto, Gerenciador de tráfego não ver o tráfego de saudação HTTP entre o cliente de saudação e servidor de saudação.

Além disso, o endereço IP de origem da saudação de consulta DNS Olá recebido pelo Gerenciador de tráfego pertence serviço DNS recursivo toohello, não o cliente hello. Portanto, o Traffic Manager não tem forma tootrack individuais clientes e não pode implementar 'Autoadesivas' sessões. Essa limitação é o tráfego de DNS com base comum de tooall sistemas de gerenciamento e não é específico tooTraffic Manager.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Por que vejo um erro de HTTP ao usar o Gerenciador de Tráfego?

Conforme explicado em [como o Gerenciador de tráfego funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), o Traffic Manager funciona no nível DNS de saudação. Ele usa o DNS respostas toodirect clientes toohello serviço apropriado ponto de extremidade. Clientes, em seguida, conecte-se ponto de extremidade de serviço toohello diretamente, não pelo Gerenciador de tráfego. O Gerenciador de Tráfego não vê o tráfego HTTP entre o cliente e o servidor. Portanto, qualquer erro HTTP visto deve ser proveniente do aplicativo. Para o aplicativo de toohello tooconnect do cliente hello, todas as etapas de resolução DNS estão completas. Isso inclui qualquer interação de Gerenciador de tráfego no fluxo de tráfego de aplicativo hello.

As investigações devem se concentrar no aplicativo hello.

cabeçalho de host de saudação HTTP enviado do navegador saudação do cliente é origem mais comum de saudação de problemas. Certifique-se de que o aplicativo hello é cabeçalho de host correto tooaccept configurado Olá Olá nome de domínio que estiver usando. Para pontos de extremidade usando hello do serviço de aplicativo do Azure, consulte [Configurando um nome de domínio personalizado para um aplicativo web no serviço de aplicativo do Azure usando o Gerenciador de tráfego](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>O que é o impacto no desempenho hello usando o Gerenciador de tráfego?

Conforme explicado em [como o Gerenciador de tráfego funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), o Traffic Manager funciona no nível DNS de saudação. Desde que os clientes se conectam a pontos de extremidade de serviço tooyour diretamente, não há nenhum impacto no desempenho ao usando o Gerenciador de tráfego de uma vez estabelecida a conexão de saudação.

Como o Traffic Manager se integra com aplicativos em nível DNS de saudação, é necessário um toobe de pesquisa DNS adicional inserido Olá cadeia de resolução DNS. impacto de saudação do Traffic Manager no tempo de resolução DNS é mínimo. O Traffic Manager usa uma rede global de servidores de nome e usa [difusão](https://en.wikipedia.org/wiki/Anycast) consultas DNS tooensure rede sempre são roteadas toohello servidor de nome disponível mais próximo. Além disso, o armazenamento em cache das respostas DNS significa latência DNS adicional Olá incorrida usando o Gerenciador de tráfego aplica-se apenas tooa fração de sessões.

rotas de método de desempenho de saudação do toohello mais próximo disponível ponto de extremidade de tráfego. Olá, resultado líquido é que hello impacto de desempenho associado a este método deve ser mínimo. Um aumento na latência DNS deve ser deslocado pela extremidade inferior do toohello de latência da rede.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>Quais protocolos de aplicativo posso usar com o Gerenciador de Tráfego?

Conforme explicado em [como o Gerenciador de tráfego funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), o Traffic Manager funciona no nível DNS de saudação. Após a conclusão da pesquisa de DNS hello, os clientes se conectam ponto de extremidade de aplicativo toohello diretamente, não pelo Gerenciador de tráfego. Portanto, a conexão de saudação pode usar qualquer protocolo de aplicativo. Se você selecionar o TCP como Olá monitoramento protocolo, Gerenciador de tráfego monitoramento de integridade do ponto de extremidade pode ser feito sem usar qualquer protocolo de aplicativo. Se você escolher a integridade de saudação toohave verificada usando um protocolo de aplicativo, o ponto de extremidade de saudação precisa toobe toorespond capaz de tooeither HTTP ou HTTPS obter solicitações.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>Posso usar o Gerenciador de Tráfego com um nome de domínio raiz?

Não. padrões DNS Olá não permitam CNAMEs tooco-existe com outros registros DNS de saudação mesmo nome. Olá ápice (ou raiz) de uma zona DNS sempre contém dois registros DNS pré-existente; Olá SOA e hello autoritativos registros NS. Isso significa que um registro CNAME não pode ser criado no ápice da zona de saudação sem violar os padrões DNS hello.

Gerenciador de tráfego exige um nome DNS do DNS CNAME toomap registro Olá banido. Por exemplo, você pode mapear contoso.trafficmanager.net de nome DNS do perfil de Gerenciador de tráfego de toohello www.contoso.com. Além disso, Olá perfil do Traffic Manager retorna um segundo tooindicate de DNS CNAME qual ponto de extremidade cliente Olá deve se conectar ao.

toowork esse problema, recomendamos o uso de um redirecionamento toodirect o tráfego HTTP de saudação naked domínio nome tooa URL diferente, que, em seguida, pode usar o Gerenciador de tráfego. Por exemplo, hello domínio naked 'contoso.com' pode redirecionar os usuários toohello CNAME 'www.contoso.com' que aponta toohello nome DNS do Traffic Manager.

O suporte completo para domínios naked no Gerenciador de Tráfego é controlado em nossa lista de pendências de recurso. Você pode registrar seu suporte para essa solicitação de recurso [votando em nosso site de comentários da comunidade](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>Gerenciador de tráfego considere endereço de sub-rede de cliente Olá ao lidar com consultas DNS? 
Não, atualmente o Traffic Manager considera apenas Olá endereço IP de origem da consulta DNS de saudação recebe, que geralmente é o endereço IP de saudação do resolvedor DNS hello, ao realizar pesquisas para métodos de roteamento geográfico e o desempenho.  
Especificamente, [RFC 7871 – a sub-rede de cliente em consultas DNS](https://tools.ietf.org/html/rfc7871) que fornece um [mecanismo de extensão para DNS (EDNS0)](https://tools.ietf.org/html/rfc2671) que pode passar no endereço de sub-rede do cliente de saudação do resolvedores compatíveis tooDNS servidores é atualmente não tem suporte no Gerenciador de tráfego. Você pode registrar seu suporte para essa solicitação de recurso por meio de nosso [site de comentários da comunidade](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>O que é o TTL do DNS e como ele afeta os meus usuários?

Quando uma consulta DNS chega no Gerenciador de tráfego, ele define um valor em resposta Olá chamada tempo de vida (TTL). Esse valor, cuja unidade é em segundos, indica tooDNS resolvedores downstream em quanto tempo toocache essa resposta. Enquanto não há garantia de resolvedores de DNS toocache esse resultado, armazená-los permite que eles toorespond tooany as consultas subsequentes Desativar cache Olá em vez de passar tooTraffic servidores DNS Manager. Isso afeta as respostas de saudação da seguinte maneira:
- um TTL mais alto reduz o número de saudação de consultas que parar em Olá servidores DNS do Traffic Manager, que podem reduzir o custo de saudação para um cliente porque o número de consultas servido é um uso faturável.
- um TTL superior pode reduzir Olá tempo toodo uma pesquisa de DNS.
- um TTL superior também significa que os dados não refletem as informações integridade mais recentes Olá que obteve Traffic Manager por meio de seus agentes probing.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>Como alto ou baixo posso definir Olá TTL de respostas do Traffic Manager?

Você pode definir em uma por nível de perfil, Olá toobe TTL do DNS como baixa como 0 segundos e de até 2.147.483.647 segundos (Olá intervalo máximo compatível com [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). TTL de 0 significa que os resolvedores DNS downstream não armazenar em cache respostas de consultas e todas as consultas são esperados tooreach servidores DNS do Traffic Manager Olá para resolução.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Método de roteamento de tráfego geográfico do Gerenciador de Tráfego

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>Quais são alguns casos de uso em que o roteamento geográfico é útil? 
Tipo de roteamento geográfico pode ser usado em qualquer cenário em que um cliente do Azure precisa toodistinguish seus usuários com base em regiões geográficas. Por exemplo, usando o método de roteamento de tráfego geográfica hello, você pode dar aos usuários de regiões específicas uma experiência de usuário diferentes daqueles de outras regiões. Outro exemplo é estar em conformidade com as normas soberanas de dados locais que exigem que os usuários de uma região específica sejam atendidos somente pelos pontos de extremidade dessa região.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>O que são regiões de saudação que são suportados pelo Gerenciador de tráfego para roteamento geográfico? 
hierarquia de país/região Olá que é usada pelo Gerenciador de tráfego pode ser encontrada [aqui](traffic-manager-geographic-regions.md). Embora essa página é mantida atualizada com as alterações, você pode recuperar também programaticamente Olá as mesmas informações usando Olá [REST API do Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>Como o Gerenciador de Tráfego determina de que região um usuário está fazendo uma consulta? 
Gerenciador de tráfego analisa Olá IP de origem da consulta de saudação (isso provavelmente é um resolvedor DNS local fazendo Olá consultando em nome de usuário de saudação) e usa um IP tooregion mapa toodetermine Olá local interno. Este mapa será atualizado em um tooaccount continuamente as alterações nas Olá internet. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>Garantia de que o Gerenciador de tráfego pode determinar corretamente Olá exata geográfica do usuário Olá em todos os casos?
Não, o Traffic Manager não pode garantir a essa região geográfica Olá é inferir de endereço de IP de origem de saudação de uma consulta DNS sempre corresponderá local do usuário toohello devido a seguir toohello motivos: 

- Primeiro, conforme descrito na pergunta anterior hello, Olá vemos é de um resolvedor DNS fazer pesquisa de saudação em nome de usuário de saudação de endereço IP de origem. Enquanto a localização geográfica de saudação do resolvedor DNS Olá é um bom proxy para localização geográfica de saudação do usuário hello, ele também pode ser diferente dependendo da superfície de saudação do serviço de resolução DNS hello e Olá determinado serviço de resolução DNS que optou por um cliente toouse. Por exemplo, um cliente localizado na Malásia poderia especificar no uso de configurações do seu dispositivo, um serviço de resolução DNS pode obter cujo servidor DNS em Cingapura escolhidas toohandle resoluções de consulta Olá para o usuário/dispositivo. Nesse caso, o Traffic Manager só pode ver IP do resolvedor Olá endereço que corresponde a toohello local Cingapura. Consulte também Olá anteriores perguntas Frequentes sobre o endereço de sub-rede do cliente suportam nesta página.

- Segundo, o Traffic Manager usa uma conversão de região do mapa interno toodo Olá endereço IP toogeographic. Enquanto o mapa é validado e atualizado em uma base contínua tooincrease sua precisão e a conta para Olá surgimento de natureza de Olá da internet, se ainda há possibilidade de saudação que nossas informações não são uma representação exata de localização geográfica de saudação de todos os endereços IP Hello.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>Toobe de necessidade de um ponto de extremidade fisicamente localizado em Olá mesma região Olá um que é configurado com roteamento geográfico? 
Não, local de saudação do ponto de extremidade de saudação impõe sem restrições nos quais regiões podem ser mapeado tooit. Por exemplo, um ponto de extremidade na região Central dos EUA Azure pode ter tooit Índia direcionada de todos os usuários.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>Eu posso atribuir regiões geográficas tooendpoints em um perfil que não está configurado o roteamento geográfico toodo? 

Sim, se o método de roteamento Olá de um perfil não estiver geográfico, você pode usar Olá [REST API do Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign regiões geográficas tooendpoints no perfil. No caso de saudação de perfis de tipo de roteamento não geográfico, essa configuração é ignorada. Se você alterar um tipo como esse perfil toogeographic roteamento em um momento posterior, o Gerenciador de tráfego pode usar esses mapeamentos.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>Por que estou recebendo um erro quando tento toochange método de roteamento de saudação de um tooGeographic perfil existente?

Todos os pontos de extremidade de saudação em um perfil com o roteamento geográfico necessário toohave pelo menos uma região mapeado tooit. tooconvert um tipo de roteamento de toogeographic perfil existente, é necessário primeiro tooassociate regiões geográficas tooall seus pontos de extremidade usando Olá [REST API do Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) antes de alterar Olá roteamento digite toogeographic. Se primeiro usando o portal, excluir pontos de extremidade hello, alterar método de roteamento de saudação do hello perfil toogeographic e, em seguida, adicionar pontos de extremidade de saudação junto com seu mapeamento de região geográfica. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>Por que é enfaticamente aconselhável que os clientes criem perfis aninhados em vez de pontos de extremidade em um perfil com o roteamento geográfico habilitado? 

Uma região pode ser atribuída tooonly um ponto de extremidade dentro de um perfil se seu usando o tipo de roteamento geográfico. Se esse ponto de extremidade não é um tipo aninhado com uma tooit de perfil anexado filho, se esse ponto de extremidade for íntegro, o Traffic Manager continuará toosend tráfego tooit desde alternativa de saudação de não enviar que qualquer tráfego não é melhor. Gerenciador de tráfego não não failover tooanother ponto de extremidade, mesmo quando a região Olá atribuída é "pai" da região de saudação atribuído toohello ponto de extremidade que deu não íntegro (por exemplo, se um ponto de extremidade que tem região Espanha fica não íntegro, que vamos não tooanother de failover ponto de extremidade que tem Olá região Europa atribuído tooit). Isso é feito tooensure que a instalação do Gerenciador de tráfego aspectos Olá fronteiras geográficas que um cliente tem em seu perfil. benefício da saudação tooget de failover do ponto de extremidade de tooanother quando um ponto de extremidade fica não íntegro, é recomendável que seja atribuída a regiões geográficas toonested perfis com vários pontos de extremidade dentro dele, em vez de pontos de extremidade individuais. Dessa forma, se um ponto de extremidade falhar de perfil filho Olá aninhado, tráfego de ponto de extremidade do failover tooanother dentro de saudação mesmo aninhados perfil filho.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>Existem restrições em versão Olá API que oferece suporte a esse tipo de roteamento?

Sim, somente a versão da API de 2017-03-01 e dá suporte a mais recente Olá geográfico tipo de roteamento. As versões mais antigas da API não podem ser usado toocreated perfis do tipo de roteamento geográfico ou atribuir tooendpoints regiões geográficas. Se uma versão mais antiga de API é usada tooretrieve perfis de uma assinatura do Azure, qualquer perfil de tipo de roteamento geográfico não é retornado. Além disso, ao usar versões de API mais antigas, todos os perfis retornados que tiverem pontos de extremidade com uma atribuição de região geográfica não terão essa atribuição exibida.



## <a name="traffic-manager-endpoints"></a>Pontos de extremidade do Gerenciador de Tráfego

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>Posso usar o Gerenciador de Tráfego com pontos de extremidade de várias assinaturas?

Não é possível usar pontos de extremidade de várias assinaturas com Aplicativos Web do Azure. Os Aplicativos Web do Azure exigem que qualquer nome de domínio personalizado usado com Aplicativos Web seja usado somente em uma única assinatura. Não é possível toouse os aplicativos Web de várias assinaturas por hello mesmo nome de domínio.

Para outros tipos de ponto de extremidade, é possível toouse Gerenciador de tráfego com pontos de extremidade de mais de uma assinatura. No Gerenciador de recursos, os pontos de extremidade de qualquer assinatura podem ser adicionados tooTraffic Manager, como pessoa Olá configuração de perfil do Gerenciador de tráfego Olá tem o ponto de extremidade de toohello de acesso de leitura. Essas permissões podem ser concedidas usando o [RBAC (controle de acesso baseado em função) do Azure Resource Manager](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>Posso usar o Gerenciador de Tráfego com os slots de “Preparo” do Serviço de Nuvem?

Sim. Os slots de “preparo” do Serviço de Nuvem podem ser configurados no Gerenciador de Tráfego como pontos de extremidade Externos. Verificações de integridade ainda são cobrado na taxa de pontos de extremidade do Azure hello. Porque Olá tipo de ponto de extremidade externo está em uso, as alterações do serviço subjacente toohello não são aplicadas automaticamente. Com pontos de extremidade externos, o Traffic Manager não pode detectar quando Olá serviço de nuvem é interrompido ou excluído. Portanto, Olá Traffic Manager continua a cobrança para verificações de integridade até que o ponto de extremidade hello está desabilitado ou excluído.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>O Gerenciador de Tráfego dá suporte aos pontos de extremidade IPv6?

No momento, o Gerenciador de Tráfego não oferece servidores de nome endereçáveis por IPv6. No entanto, o Traffic Manager ainda pode ser usado por clientes IPv6 tooIPv6 pontos de extremidade de conexão. Um cliente não faz solicitações de DNS diretamente tooTraffic Manager. Em vez disso, o cliente Olá usa um serviço DNS recursivo. Um cliente somente IPv6 envia solicitações de serviço DNS recursivo toohello via IPv6. Em seguida, serviço recursivo de saudação deve ser servidores de nome toocontact capaz de saudação do Traffic Manager usando IPv4.

Gerenciador de tráfego responde com o nome DNS de saudação do ponto de extremidade de saudação. ponto de extremidade toosupport um IPv6, um DNS AAAA registre apontando Olá ponto de extremidade DNS nome toohello IPv6 endereço deve existir. Verificações de integridade do Gerenciador de Tráfego dão suporte apenas a endereços IPv4. serviço Hello precisa tooexpose um IPv4 de ponto de extremidade em Olá mesmo nome DNS.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>Posso usar o Gerenciador de tráfego com mais de um aplicativo Web de saudação mesma região?

Normalmente, o Gerenciador de tráfego é usado toodirect tráfego tooapplications implantado em regiões diferentes. No entanto, ele também pode ser usado onde um aplicativo tem mais de uma implantação em Olá mesma região. Olá pontos de extremidade do Azure Traffic Manager permite mais de um ponto de extremidade do aplicativo Web de saudação mesmo toobe de região do Azure adicionados toohello mesmo perfil do Gerenciador de tráfego.

##  <a name="traffic-manager-endpoint-monitoring"></a>Monitoramento de ponto de extremidade do Gerenciador de Tráfego

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>Falhas de região está tooAzure resiliente Traffic Manager?

O Traffic Manager é um componente fundamental de entrega de saudação de aplicativos altamente disponíveis no Azure.
toodeliver alta disponibilidade, o Traffic Manager deve ter um nível muito alto de disponibilidade e ser resiliente tooregional falha.

Por design, os componentes de Gerenciador de tráfego são resilientes tooa falha completa de qualquer região do Azure. Este resiliência se aplica a componentes do Gerenciador de tráfego tooall: servidores de nome DNS hello, Olá API, camada de armazenamento de saudação e ponto de extremidade de saudação serviço de monitoramento.

Olá improvável de uma interrupção de uma região do Azure inteira, Gerenciador de tráfego é esperado toocontinue toofunction normalmente. Aplicativos implantados em várias regiões do Azure podem confiar na instância disponível do Gerenciador de tráfego toodirect tráfego tooan de seu aplicativo.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>Como a escolha de saudação do local do grupo de recursos afeta Traffic Manager?

O Gerenciador de Tráfego é um serviço global único. Não é regional. Escolha de saudação do local do grupo de recurso não torna nenhum perfil do Gerenciador de diferença tooTraffic implantados nesse grupo de recursos.

Gerenciador de recursos do Azure requer que todos os toospecify de grupos de recursos um local, que determina o local padrão Olá recursos implantados nesse grupo de recursos. Quando você cria um perfil do Gerenciador de Tráfego, ele é criado em um grupo de recursos. Todos os perfis do Gerenciador de tráfego usar **global** como sua localização, substituindo saudação padrão de grupo de recursos.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>Como determinar o estado atual de saudação de cada ponto de extremidade?

Olá monitorar o status de cada ponto de extremidade atual, em adição toohello perfil geral, é exibido no hello portal do Azure. Essas informações também estão disponíveis via Olá Monitor de tráfego [API REST](https://msdn.microsoft.com/library/azure/mt163667.aspx), [cmdlets do PowerShell](https://msdn.microsoft.com/library/mt125941.aspx), e [CLI do Azure de plataforma cruzada](../cli-install-nodejs.md).

Azure não fornece informações históricas sobre o ponto de extremidade anterior integridade ou hello alertas tooraise de capacidade sobre integridade de tooendpoint alterações.

### <a name="can-i-monitor-https-endpoints"></a>Posso monitorar os pontos de extremidade HTTPS?

Sim. O Gerenciador de Tráfego oferece suporte à investigação por HTTPS. Configurar **HTTPS** como protocolo de saudação na configuração de monitoramento de saudação.

O Gerenciador de Tráfego não pode fornecer nenhuma validação de certificado, incluindo:

* Certificados no lado do servidor não estão validados
* Certificados no lado do servidor SNI não estão validados
* Não há suporte para certificados de cliente

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>Posso usar o Gerenciador de Tráfego mesmo se o aplicativo não tiver suporte para HTTP ou HTTPS?

Sim. Você pode especificar TCP como Olá protocolo e o Gerenciador de tráfego de monitoramento pode iniciar uma conexão TCP e aguardar uma resposta do ponto de extremidade de saudação. Se o ponto de extremidade Olá responder toohello solicitação de conexão com uma conexão de saudação do tooestablish de resposta, no tempo limite de saudação período e, em seguida, esse ponto de extremidade está marcado como íntegro.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>Quais respostas específicas são necessárias do ponto de extremidade de saudação ao usar TCP monitoramento?

Quando o monitoramento de TCP é usado, o Traffic Manager inicia um handshake TCP de três vias enviando um SYN solicitação tooendpoint em Olá porta especificada. Em seguida, ele espera por um período de tempo (como especificado nas configurações de tempo limite de saudação) por uma resposta do ponto de extremidade de saudação. Se o ponto de extremidade Olá responde toohello SYN solicitação com uma resposta de SYN ACK dentro do período de espera de saudação especificado nas configurações de monitoramento de saudação e esse ponto de extremidade será considerado íntegro. Se Olá resposta SYN ACK for recebida, Olá Traffic Manager redefine conexão Olá respondendo novamente com uma primeira.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>Com qual velocidade o Gerenciador de Tráfego move meus usuários para fora de um ponto de extremidade não íntegro?

O Traffic Manager fornece várias configurações que podem ajudá-lo toocontrol comportamento de failover de saudação do seu perfil do Gerenciador de tráfego da seguinte maneira:
- Você pode especificar que Olá Traffic Manager investigações Olá pontos de extremidade com mais frequência, definindo Olá intervalo de sondagem em 10 segundos. Isso garante que qualquer ponto de extremidade que esteja ficando não íntegro possa ser detectado assim que possível. 
- Você pode especificar quanto tempo expira toowait antes de uma solicitação de verificação de integridade (valor de tempo limite mínimo é 5 segundos).
- Você pode especificar quantas falhas podem ocorrer antes que o ponto de extremidade hello está marcado como não íntegro. Esse valor pode ser baixa como 0, na qual ponto de extremidade Olá caso é marcado como não íntegro assim que ele não consegue Olá verificação de integridade do primeiro. No entanto, usando o valor mínimo de saudação de 0 para número de saudação tolerado de falhas pode causar tooendpoints sendo retirada da rotação devido tooany problemas temporários que podem ocorrer em tempo de saudação de sondagem.
- Você pode especificar Olá time-to-live (TTL) para Olá DNS resposta toobe baixa como 0. Isso significa que resolvedores de DNS não é possível armazenar em cache resposta hello e cada nova consulta obtém uma resposta que incorpora informações de integridade mais atualizadas Olá que Olá Traffic Manager tem.

Usando essas configurações, o Traffic Manager pode fornecer failovers menos de 10 segundos depois que um ponto de extremidade fica não íntegro e uma consulta DNS é feita no perfil de saudação correspondente.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>Como especificar diferentes configurações de monitoramento para diferentes pontos de extremidade em um perfil?

As configurações de monitoramento do Gerenciador de Tráfego estão em um nível por perfil. Se você precisar toouse uma configuração de monitoramento diferente para apenas um ponto de extremidade, isso pode ser feito por ter esse ponto de extremidade como um [aninhados perfil](traffic-manager-nested-profiles.md) cujas configurações de monitoramentos são diferentes do perfil do hello pai.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>Qual cabeçalho host as verificações de integridade do ponto de extremidade usam?

O Gerenciador de Tráfego usa cabeçalhos de host em verificações de integridade HTTP e HTTPS. cabeçalho de host Olá usado pelo Gerenciador de tráfego é o nome de saudação do destino de ponto de extremidade de saudação configurado no perfil de saudação. valor de saudação usado no cabeçalho de host Olá não pode ser especificado separadamente da propriedade de destino de saudação.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>Quais são os endereços IP de saudação do qual Olá verificações de integridade se originam?

Olá lista a seguir contém endereços IP de saudação do qual o Traffic Manager verificações de integridade podem ser obtidos. Você pode usar essa lista tooensure conexões de entrada desses endereços IP são permitidas em Olá pontos de extremidade toocheck seu status de integridade.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>Ponto de extremidade toomy verificações de quantos integridade posso esperar do Gerenciador de tráfego?

número de saudação de integridade do Traffic Manager verifica atingir seu ponto de extremidade depende do seguinte hello:
- Olá valor que você definiu para o intervalo de monitoramento da saudação (intervalo menor significa que mais solicitações inicial no ponto de extremidade em um período de tempo determinado).
- número de saudação de locais de verificações de integridade Olá origem (endereços IP de saudação de onde você pode esperar essas verificações é listado na saudação anterior perguntas Frequentes).

## <a name="traffic-manager-nested-profiles"></a>Perfis aninhados do Gerenciador de Tráfego

### <a name="how-do-i-configure-nested-profiles"></a>Como posso configurar perfis aninhados?

Perfis do Gerenciador de tráfego aninhados podem ser configurados usando ambos os hello Azure Resource Manager e Olá clássico APIs de REST do Azure, cmdlets do PowerShell do Azure e os comandos de CLI do Azure de plataforma cruzada. Eles também têm suporte por meio do novo portal do Azure hello. Eles não têm suporte no portal clássico do hello.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>A quantas camadas de aninhamento o Gerenciador de Tráfego dá suporte?

Você pode aninhar perfis de too10 níveis de profundidade. “Loops” não são permitidos.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>Posso combinar outros tipos de ponto de extremidade com perfis filho aninhadas, no mesmo perfil do Gerenciador de tráfego de Olá?

Sim. Não há nenhuma restrição sobre como combinar os pontos de extremidade de diferentes tipos em um perfil.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>Como o modelo de cobrança Olá se aplicam para perfis aninhados?

Há não impacto negativo sobre os preços ao usar perfis aninhados.

A cobrança do Gerenciador de Tráfego tem dois componentes: verificações de integridade do ponto de extremidade e milhões de consultas DNS

* Verificações de integridade de ponto de extremidade: não há nenhum encargo para um perfil filho quando configurado como um ponto de extremidade em um perfil pai. Monitoramento de pontos de extremidade de saudação no perfil filho de saudação é cobrado em Olá maneira normal.
* Consultas DNS: cada consulta é contada apenas uma vez. Uma consulta em relação a um perfil pai que retorna um ponto de extremidade de um perfil filho é contada em relação a saudação pai perfil.

Para obter detalhes completos, consulte Olá [página de preços do Gerenciador de tráfego](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>Há impacto no desempenho para perfis aninhados?

Nº Não há nenhum impacto no desempenho ao usar perfis aninhados.

servidores de nome do Gerenciador de tráfego Olá atravessam hierarquia de perfil Olá internamente durante o processamento de cada consulta DNS. Um perfil do DNS consulta tooa pai pode receber uma resposta DNS com um ponto de extremidade de um perfil filho. Um único registro CNAME é usado se você está usando um único perfil ou perfis aninhados. Não há nenhuma necessidade toocreate um registro CNAME para cada perfil na hierarquia de saudação.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>Como o Gerenciador de tráfego computação integridade Olá de um ponto de extremidade aninhado em um perfil pai?

perfil do pai de saudação não executa verificações de integridade no filho Olá diretamente. Em vez disso, integridade Olá de pontos de extremidade do perfil do hello filho são usados toocalculate Olá a integridade geral do perfil do hello filho. Essas informações são propagadas Olá aninhado perfil hierarquia toodetermine Olá da integridade do ponto de extremidade de saudação aninhada. perfil de pai de saudação usa esse toodetermine integridade agregada se tráfego Olá pode ser direcionado toohello filho.

Olá tabela a seguir descreve o comportamento de saudação do Traffic Manager verificações de integridade para um ponto de extremidade aninhado.

| Status do Monitor de perfil filho | Status do monitor de ponto de extremidade pai | Observações |
| --- | --- | --- |
| Desabilitado. perfil de filho Olá foi desabilitado. |Parada |estado de ponto de extremidade pai Olá for interrompido, não desabilitado. Olá estado desabilitado é reservado para indicar que você desativou o ponto de extremidade Olá no perfil do hello pai. |
| Degradado. Pelo menos um ponto de extremidade do perfil filho está no estado Degradado. |Online: o número de saudação de pontos de extremidade Online no perfil filho de saudação é pelo menos Olá o valor de MinChildEndpoints.<BR>Verificando ponto de extremidade: o número de saudação de pontos de extremidade CheckingEndpoint plus Online no perfil filho de saudação é pelo menos Olá o valor de MinChildEndpoints.<BR>Degradado: caso contrário. |O tráfego é roteado tooan de ponto de extremidade do status CheckingEndpoint. Se minchildendpoints for muito alto, o ponto de extremidade de saudação sempre está degradado. |
| Online. Pelo menos, um ponto de extremidade do perfil filho está em um estado Online. Nenhum ponto de extremidade é Olá estado degradado. |Veja acima. | |
| CheckingEndpoints. Pelo menos, um ponto de extremidade do perfil filho é um 'CheckingEndpoint'. Nenhum ponto de extremidade está ‘Online’ ou ‘Degradado’ |Mesmo que acima. | |
| Inativo. Todos os pontos de extremidade de perfil filho estão com status Desabilitado ou Parado ou esse é um perfil que não tem nenhum ponto de extremidade. |Parada | |

## <a name="next-steps"></a>Próximas etapas:
- Saiba mais sobre o [failover automático e monitoramento do ponto de extremidade](../traffic-manager/traffic-manager-monitoring.md)do Gerenciador de Tráfego.
- Saiba mais sobre os [métodos de roteamento de tráfego](../traffic-manager/traffic-manager-routing-methods.md)do Gerenciador de Tráfego.