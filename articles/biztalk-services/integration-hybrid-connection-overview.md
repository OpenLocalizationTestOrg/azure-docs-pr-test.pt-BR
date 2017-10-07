---
title: "Visão geral das conexões de aaaHybrid | Microsoft Docs"
description: "Saiba mais sobre Conexões Híbridas, segurança, portas TCP e configurações com suporte. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>Visão geral de Conexões Híbridas

> [!IMPORTANT]
> As Conexões Híbridas do BizTalk foram desativadas e substituídas pelas Conexões Híbridas do Serviço de Aplicativo. Para obter mais informações, incluindo como toomanage as conexões existentes de híbrida do BizTalk, consulte [conexões híbridas dos serviços de aplicativo do Azure](../app-service/app-service-hybrid-connections.md).

Introdução tooHybrid conexões, lista de configurações de saudação com suporte, e listas Olá portas TCP necessárias.

## <a name="what-is-a-hybrid-connection"></a>O que é uma conexão híbrida
As Conexões Híbridas são um recurso dos Serviços BizTalk do Azure. Conexões híbridas fornecem um maneira fácil e conveniente tooconnect Olá aplicativos Web recursos no serviço de aplicativo do Azure (anteriormente conhecida como sites da Web) e Olá aplicativos móveis em recursos do serviço de aplicativo do Azure (anteriormente conhecida como serviços móveis) local tooon por trás do firewall.

![Conexões Híbridas][HCImage]

Os benefícios das Conexões Híbridas incluem:

* Aplicativos Web e Aplicativos Móveis podem acessar, com segurança, serviços e dados locais existentes.
* Vários aplicativos Web ou aplicativos móveis podem compartilhar uma Conexão híbrida de tooaccess um recurso local.
* As portas TCP mínimo são tooaccess necessário em sua rede.
* Aplicativos que usam conexões híbridas acessam apenas recursos de local específico Olá publicado por meio de Olá Conexão híbrida.
* Pode se conectar a recursos de local de tooany que usa uma porta TCP estática, como SQL Server, MySQL, APIs da Web de HTTP e a maioria dos serviços da Web personalizados.
  
  > [!NOTE]
  > Serviços baseados em TCP que utilizam portas dinâmicas (como um Modo passivo de FTP ou Modo passivo estendido) não têm suporte atualmente. O LDAP também não tem suporte. O LDAP usa uma porta TCP estática, mas também poderia usar UDP. Como resultado, não há suporte.
  > 
  > 
* Podem ser utilizados com todas as estruturas com suporte nos Aplicativos Web (.NET, PHP, Java, Python, Node.js) e Aplicativos Móveis (Node.js, .NET).
* Aplicativos Web e aplicativos móveis podem acessar recursos locais em exatamente Olá mesma forma como se Olá Web ou aplicativo móvel está localizado em sua rede local. Olá, por exemplo, a mesma cadeia de caracteres de conexão usados no local também podem ser usados no Azure.

Conexões híbridas também fornecem a administradores de empresa com o controle e visibilidade de recursos corporativos de saudação acessados por aplicativos híbridos, incluindo:

* Configurações de política de grupo, os administradores podem permitir conexões híbridas Olá rede e também designar recursos que podem ser acessados por aplicativos híbridos.
* Logs de eventos e de auditoria na rede corporativa Olá dar visibilidade a recursos de saudação acessados por conexões híbridas.

## <a name="example-scenarios"></a>Cenários de exemplo
Conexões híbridas suportam Olá combinações de framework e aplicativos a seguir:

* .NET framework acesso tooSQL Server
* Serviços do .NET framework acesso tooHTTP/HTTPS com WebClient
* PHP acesso tooSQL Server, MySQL
* Java acesso tooSQL Server, Oracle e MySQL
* Serviços de acesso à Java tooHTTP/HTTPS

Ao usar conexões híbridas tooaccess local do SQL Server, considere o seguinte de saudação:

* Express chamado instâncias do SQL deve ser portas estáticas toouse configurado. Por padrão, as instâncias nomeadas como SQL Express utilizam portas dinâmicas.
* As instâncias padrão do SQL Express utilizam uma porta estática, mas o TCP precisa estar habilitado. Por padrão, o uso de TCP não está habilitado.
* Ao usar grupos de disponibilidade ou de Clustering, Olá `MultiSubnetFailover=true` modo não é suportado atualmente.
* Olá `ApplicationIntent=ReadOnly` não é suportado atualmente.
* Autenticação do SQL podem ser necessária como método de autorização de ponta a ponta Olá Olá aplicativo do Azure e Olá local SQL server com suporte.

## <a name="security-and-ports"></a>Segurança e portas
Conexões híbridas usam conexões de saudação de toosecure de autorização de assinatura de acesso compartilhado (SAS) de saudação do Azure hello e aplicativos locais Conexão do Gerenciador de Conexão híbrida toohello híbrida. Chaves de conexão separadas são criadas para o aplicativo hello e Olá Gerenciador de Conexão híbrida local. É possível fazer a rolagem por essas chaves de conexão e revogá-las de modo independente.

Conexões híbridas fornecem distribuição direta e segura de aplicativos de toohello chaves hello e Olá Gerenciador de Conexão híbrida local.

Consulte [Criar e gerenciar Conexões Híbridas](integration-hybrid-connection-create-manage.md).

*Autorização do aplicativo é separada do hello Conexão híbrida*. Qualquer método adequado de autorização pode ser usado. método de autorização Hello depende de métodos de autorização de ponta a ponta de saudação suportados entre hello nuvem do Azure e componentes de locais de saudação. Por exemplo, o seu aplicativo do Azure acessa um SQL Server local. Nesse cenário, a autorização do SQL pode ser método autorização Olá de ponta a ponta com suporte.

#### <a name="tcp-ports"></a>Portas TCP
Conexões Híbridas exigem somente conectividade TCP ou HTTP de saída da sua rede privada. Você não precisa de nenhuma porta de firewall de tooopen ou altere sua tooallow de configuração de perímetro de rede a conectividade de qualquer entrada em sua rede.

Olá portas TCP a seguir é usada por conexões híbridas:

| Porta | Por que você precisa disto |
| --- | --- |
| 9350 - 9354 |Essas portas são usadas para a transmissão de dados. Gerenciador de retransmissão de barramento de serviço Olá sondas de porta 9350 toodetermine se a conectividade TCP está disponível. Quando está disponível, ele pressupõe que a porta 9352 também está. O tráfego de dados passa pela porta 9352. <br/><br/>Permita conexões de saída portas toothese. |
| 5671 |Quando a porta 9352 é usada para tráfego de dados, porta 5671 é usada como o canal de controle de saudação. <br/><br/>Permita conexões de saída toothis porta. |
| 80, 443 |Essas portas são usadas para alguns tooAzure de solicitações de dados. Além disso, se as portas 9352 e 5671 não são utilizáveis, *, em seguida,* portas 80 e 443 são Olá fallback usado para transmissão de dados e o canal de controle de saudação.<br/><br/>Permita conexões de saída portas toothese. <br/><br/>**Observação** não é recomendável toouse esses como Olá fallbacks portas no lugar de saudação outras portas TCP. Olá HTTP/WebSocket é usado como protocolo de saudação em vez de TCP nativo para canais de dados. Isso poderia degradar o desempenho. |

## <a name="next-steps"></a>Próximas etapas
[Create and manage Hybrid Connections](integration-hybrid-connection-create-manage.md)<br/>
[Conecte-se a aplicativos Web do Azure tooan recurso local](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Conecte-se o SQL Server local tooon de um aplicativo web do Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>Consulte também
[API REST para gerenciar serviços BizTalk no Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md)<br/>
[Criar um Serviço BizTalk usando o portal do Azure](biztalk-provision-services.md)<br/>
[Serviços BizTalk: guias Painel, Monitor e Escala](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
