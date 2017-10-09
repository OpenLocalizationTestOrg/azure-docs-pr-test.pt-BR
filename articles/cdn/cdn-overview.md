---
title: "Visão geral da CDN do aaaAzure | Microsoft Docs"
description: "Saiba quais Olá é de rede de fornecimento de conteúdo (CDN) do Azure e como toouse-toodeliver conteúdo de alta largura de banda armazenando em cache blobs e conteúdo estático."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Visão geral de hello Azure Content Delivery Network (CDN)
> [!NOTE]
> Este documento descreve quais hello Azure Content Delivery Network (CDN) é, como ele funciona e recursos de saudação de cada produto de CDN do Azure.  Se você quiser que essas informações tooskip e vá reta tooa tutorial sobre como toocreate um ponto de extremidade CDN, consulte [usando o Azure CDN](cdn-create-new-endpoint.md).  Se você quiser toosee uma lista de locais de nó CDN atuais, consulte [Azure CDN POP locais](cdn-pop-locations.md).
> 
> 

Olá rede de fornecimento de conteúdo (CDN) do Azure armazena em cache o conteúdo estático da web em locais estrategicamente colocados tooprovide taxa de transferência máxima para entregar conteúdo toousers.  Olá CDN oferece aos desenvolvedores uma solução global para distribuir o conteúdo de alta largura de banda por armazenar em cache o conteúdo de saudação em nós físicos em Olá, mundo. 

Olá benefícios do uso de ativos de site da web hello CDN toocache incluem:

* Melhor desempenho e experiência de usuário para usuários finais, especialmente quando o uso de aplicativos em que várias viagens são necessários conteúdo tooload.
* Grande escala toobetter identificador alta carga instantânea, como iniciar o evento no início de saudação de um produto.
* Ao distribuir solicitações de usuário e que atende ao conteúdo dos servidores de borda, menos tráfego é enviado toohello origem.

## <a name="how-it-works"></a>Como ele funciona
![Visão geral da CDN](./media/cdn-overview/cdn-overview.png)

1. Uma usuária (Brenda) solicita um arquivo (também chamado de ativo) usando uma URL com um nome de domínio especial, como `<endpointname>.azureedge.net`.  Local de ponto de presença (POP) melhor desempenho do hello solicitação toohello a rota do DNS.  Geralmente, isso é Olá POP é usuário do toohello geograficamente mais próximo.
2. Se servidores de borda Olá Olá POP não tiverem o arquivo hello em seu cache, o servidor de borda de saudação solicitações arquivo hello origem hello.  origem de saudação pode ser um aplicativo Web do Azure, o serviço de nuvem do Azure, conta de armazenamento do Azure ou qualquer servidor web acessível publicamente.
3. origem de saudação retorna o servidor de borda do hello arquivo toohello, incluindo os cabeçalhos HTTP opcionais que descreve Time-to-Live do arquivo hello (TTL).
4. servidor de borda Olá armazena em cache o arquivo hello e retorna o solicitante original de toohello arquivo da saudação (Alice).  arquivo Hello permanece em cache no servidor de borda Olá até Olá TTL expira.  Se a origem de saudação não especificar um TTL, TTL padrão de saudação é sete dias.
5. Usuários adicionais podem Olá solicitação mesmo arquivo usando essa mesma URL e também pode ser direcionado toothat mesmo POP.
6. Se hello TTL para arquivo hello ainda não expirou, o servidor de borda de saudação retorna arquivo hello do cache de saudação.  Isso resulta em uma experiência de usuário mais rápida e responsiva.

## <a name="azure-cdn-features"></a>Recursos da Azure CDN
Há três produtos Azure CDN: **Azure CDN Standard do Akamai**, **Azure CDN Standard da Verizon** e **Azure CDN Premium da Verizon**.  Olá tabela a seguir lista os recursos de saudação disponíveis em cada produto.

|  | Akamai Standard | Verizon Standard | Verizon Premium |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Recursos de Desempenho e Otimizações__ |
| [Aceleração Dinâmica do Site](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Aceleração de Site Dinâmico - Compactação de Imagem Adaptável](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Aceleração de Site Dinâmico - Pré-busca de objeto](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Otimização do Streaming de Vídeo](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Otimização de Arquivos Grandes](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Balanceamento de Carga do Servidor Global (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Limpeza rápida](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Pré-carregamento de ativos](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [Cache de cadeia de caracteres de consulta](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Pilha dupla IPv4/IPv6 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Suporte do HTTP/2](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Segurança__ |
| Suporte ao protocolo HTTPS com o ponto de extremidade CDN |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [HTTPS de domínio personalizado](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Suporte a nome de domínio personalizado](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Filtragem geográfica](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Autenticação de token](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [Proteção DDOS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Análises e Relatórios__ |
| [Análise principal](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Relatórios avançados de HTTP](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Estatísticas em tempo real](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Alertas em tempo real](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Fácil de Usar__ |
| Fácil integração com os serviços do Azure, como [Armazenamento](cdn-create-a-storage-account-with-cdn.md), [Serviços de Nuvem](cdn-cloud-service-with-cdn.md), [Aplicativos Web](../app-service-web/app-service-web-tutorial-content-delivery-network.md) e [Serviços de Mídia](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Gerenciamento via [API REST](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md) ou [PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Mecanismo de distribuição de conteúdo personalizável e baseado em regras](cdn-rules-engine.md) | | |**&#x2713;** |
| Configurações de cache/cabeçalho (usando o [mecanismo de regras](cdn-rules-engine.md)) | | |**&#x2713;** |
| Redirecionamento/reconfiguração de URL (usando o [mecanismo de regras](cdn-rules-engine.md)) | | |**&#x2713;** |
| Regras de dispositivo móvel (usando o [mecanismo de regras](cdn-rules-engine.md)) | | |**&#x2713;** |

\*A Verizon dá suporte à entrega de arquivos grandes e mídia diretamente via Distribuição na Web Geral.


> [!TIP]
> Há um recurso que você gostaria que toosee na CDN do Azure?  [Forneça comentários](https://feedback.azure.com/forums/169397-cdn)! 
> 
> 

## <a name="next-steps"></a>Próximas etapas
tooget iniciado com a CDN, consulte [usando o Azure CDN](cdn-create-new-endpoint.md).

Se você for um cliente CDN existente, agora você pode gerenciar seus pontos de extremidade CDN através de saudação [portal do Microsoft Azure](https://portal.azure.com) ou com [PowerShell](cdn-manage-powershell.md).

toosee Olá CDN em ação, confira Olá [vídeo de nossa sessão 2016 compilação](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Saiba como tooautomate CDN do Azure com [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).

Para obter informações sobre preços, confira [Preços da CDN](https://azure.microsoft.com/pricing/details/cdn/).

