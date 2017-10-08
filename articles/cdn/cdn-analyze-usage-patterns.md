---
title: "padrões de uso do Azure CDN aaaAnalyze | Microsoft Docs"
description: "Você pode exibir os padrões de uso para o CDN usando Olá relatórios a seguir: largura de banda, os dados transferidos, ocorrências, status do Cache, a taxa de acertos de Cache, IPV4/IPV6 dados transferidos."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Analisar os padrões de uso da CDN do Azure

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Guia de saudação abaixo atravessa Olá etapas tooview Olá core relatórios por meio do portal de gerenciamento Olá Verizon perfis de. Você também pode exportar toostorage de dados de análise de núcleo, hub de eventos ou análise de logs (oms) para os perfis Verizon e Akamai [por meio do portal do azure de saudação](cdn-log-analysis.md).

Você pode exibir os padrões de uso para o CDN usando Olá relatórios a seguir:

* Largura de banda
* Dados Transferidos
* Acertos
* Status do Cache
* Taxa de Acertos do Cache
* Dados IPv4/IPV6 Transferidos

## <a name="accessing-core-reports"></a>Acessando relatórios principais
1. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-reports/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
2. Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **relatórios principais** flutuante.  Clique no relatório de saudação desejado no menu de saudação.
   
    ![Portal de gerenciamento da CDN - menu Relatórios Principais](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Largura de banda
relatório de largura de banda Olá consiste em uma tabela de dados e de gráfico que indica o uso de largura de banda Olá para HTTP e HTTPS em um período de tempo específico. Você pode exibir o uso de largura de banda de saudação em todos os POPs de CDN ou um POP específico. Isso permite que você tooview Olá tráfego picos e a distribuição entre POPs de CDN em Mbps.

* Selecione o tráfego de toosee todos os nós de borda de todos os nós ou um região/nó específico na lista suspensa hello.
* Selecionar dados de tooview de intervalo de data de hoje/esta semana/mês, etc. ou inserir datas personalizadas, clique em "Ir" toomake se que a seleção está atualizada.
* Você pode exportar e baixar dados de saudação clicando Olá localizado ao lado do ícone de planilha do excel muito "Ir".

relatório de saudação é atualizado a cada 5 minutos.

![Relatório Largura de banda](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Dados Transferidos
Este relatório consiste em uma tabela de dados e de gráfico indicando o uso de tráfego de saudação para HTTP e HTTPS em um período de tempo específico. Você pode exibir o uso de tráfego de saudação em todos os POPs de CDN ou um POP específico. Isso permite que você tooview Olá tráfego picos e a distribuição entre POPs de CDN em GB.

* Selecione o tráfego de toosee todos os nós de borda de todas as anotações ou um região/nó específico na lista suspensa hello.
* Selecionar dados de tooview de intervalo de data de hoje/esta semana/mês, etc. ou inserir datas personalizadas, clique em "Ir" toomake se que a seleção está atualizada.
* Você pode exportar e baixar dados de saudação clicando Olá localizado ao lado do ícone de planilha do excel muito "Ir".

relatório de saudação é atualizado a cada 5 minutos.

![Relatório Dados transferidos](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Acertos (códigos de status)
Este relatório descreve a distribuição de saudação de códigos de status de solicitação para o seu conteúdo. Todas as solicitações de conteúdo gerarão um código de status HTTP. código de status de saudação descreve como a borda POPs tratada solicitação hello. Por exemplo, códigos de status de 2xx indicam que a solicitação Olá foi servida com êxito tooa cliente, enquanto um código de status 4xx indica que ocorreu um erro. Para obter mais detalhes sobre o código de status HTTP, consulte [códigos de status](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Selecionar dados de tooview de intervalo de data de hoje/esta semana/mês, etc. ou inserir datas personalizadas, clique em "Ir" toomake se que a seleção está atualizada.
* Você pode exportar e baixar dados de saudação clicando Olá localizada ao lado de folha do excel muito "Ir".

![Relatório Acertos](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Status do Cache
Este relatório descreve a distribuição de saudação de acertos do cache e erros de cache de solicitação do cliente. Desde que o desempenho mais rápido Olá vierem de acertos do cache, você pode otimizar dados velocidades de entrega minimizar erros de cache e de acertos do cache expirada. Erros de cache podem ser reduzidos configurando seu tooavoid do servidor de origem atribuindo cabeçalhos de resposta "no-cache", evitando o cache de cadeia de caracteres de consulta exceto onde são estritamente necessárias e, evitando códigos de resposta não armazenável em cache. Expirado acertos podem ser evitados fazendo max-age um ativo como possíveis toominimize Olá número do servidor de origem toohello solicitações de cache.

![Relatório Status do cache](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Os status do cache principal incluem:
* TCP_HIT: servido da Borda. objeto Olá estava no cache e não excedeu sua idade máxima.
* TCP_MISS: servido da Origem. objeto Olá não estava no cache e resposta Olá foi tooorigin voltar.
* TCP_EXPIRED _MISS: Servido da origem após revalidação com a origem. objeto Olá estava no cache, mas excedeu sua idade máxima. A revalidação com origem resultou no objeto de cache hello está sendo substituído por uma nova resposta de origem.
* TCP_EXPIRED _HIT: servido do Edge após revalidação com a origem. objeto Olá estava no cache, mas excedeu sua idade máxima. A revalidação no servidor de origem Olá resultou no objeto de cache Olá sendo sem modificações.
* Selecionar dados de tooview de intervalo de data de hoje/esta semana/mês, etc. ou inserir datas personalizadas, clique em "Ir" toomake se que a seleção está atualizada.
* Você pode exportar e baixar dados de saudação clicando Olá localizado ao lado do ícone de planilha do excel muito "Ir".

### <a name="full-list-of-cache-statuses"></a>Lista completa de status do cache
* TCP_HIT - esse status é relatado quando uma solicitação é atendida diretamente do cliente de toohello Olá POP. Um ativo é atendido imediatamente de um POP quando ele é armazenado em cache no cliente de toohello Olá POP mais próximo e tem uma validade time-to-live, ou o TTL. TTL é determinado pelo Olá cabeçalhos de resposta a seguir:
  
  * Cache-Control: período máximo s
  * Cache-Control: período máximo
  * Expira
* TCP_MISS - este status indica que uma versão em cache do ativo de saudação solicitado não foi encontrada no cliente de toohello Olá POP mais próximo. ativo de saudação será solicitado de um servidor de origem ou um servidor de proteção de origem. Se o servidor de origem hello ou servidor de proteção de origem Olá retorna um ativo, ele será servido toohello cliente e armazenadas em cache no cliente hello e o servidor de borda de saudação. Caso contrário, um código de status diferente de 200 (por exemplo, 403 Proibido, 404 Não Encontrado etc.) será retornado.
* TCP_EXPIRED _HIT - esse status é relatado quando recebeu uma solicitação de destino de um ativo com um TTL expirado, como quando a idade máxima do ativo Olá tiver expirado, diretamente do cliente de toohello Olá POP.
  
    Uma solicitação expirada normalmente resulta em um servidor de origem de toohello de solicitação de revalidação. Em ordem para um toooccur _HIT TCP_EXPIRED, o servidor de origem de Olá deve indicar que não existe uma versão mais recente do ativo de saudação. Esse tipo de situação normalmente atualizará os cabeçalhos Cache-Control e Expires do ativo.
* TCP_EXPIRED _MISS - esse status é relatado quando uma versão mais recente de um ativo em cache expirada é fornecida de cliente de toohello Olá POP. Isso ocorre quando a saudação TTL para um ativo em cache expirou (por exemplo, expirado idade máxima) e o servidor de origem Olá retorna uma versão mais recente esse ativo. Essa nova versão do ativo Olá será servido cliente toohello em vez da versão armazenada em cache hello. Além disso, ele será ser armazenado em cache no servidor de borda hello e cliente de saudação.
* CONFIG_NOCACHE - esse status indica que uma configuração específica do cliente em nossos borda POP impediu ativo Olá sendo armazenada em cache.
* NONE - esse status indica que uma verificação de atualização de conteúdo do cache não foi executada.
* TCP_ CLIENT_REFRESH _MISS - esse status é relatado quando um cliente HTTP (por exemplo, o navegador) força uma tooretrieve borda POP uma nova versão de um ativo obsoleto do servidor de origem de saudação.
  
    Por padrão, nossos servidores impedir que um cliente HTTP a imposição de nossos servidores de borda tooretrieve uma nova versão do ativo de saudação do servidor de origem de saudação.
* TCP_ PARTIAL_HIT - esse status é relatado quando uma solicitação de intervalo de bytes resulta em um acerto de um ativo parcialmente armazenado em cache. Olá solicitou o intervalo de bytes imediatamente é fornecido de cliente de toohello POP hello.
* UNCACHEABLE - esse status é relatado quando o controle de Cache de um ativo e expira indica que ele deve não ser armazenado em cache em um POP ou pelo cliente Olá HTTP. Esses tipos de solicitações são atendidos do servidor de origem Olá

## <a name="cache-hit-ratio"></a>Taxa de Acertos do Cache
Este relatório indica a porcentagem de saudação do cache de solicitações que foram atendidas diretamente do cache.

relatório de saudação fornece Olá detalhes a seguir:

* Olá solicitou o conteúdo foi armazenado em cache solicitante de toohello Olá POP mais próximo.
* Olá solicitação foi servida diretamente da borda de saudação da rede.
* solicitação de saudação não exige revalidação no servidor de origem de saudação.

relatório de saudação não incluem:

* Solicitações negadas devido toocountry opções de filtragem.
* Solicitações de ativos cujos cabeçalhos indicam que eles não devem ser armazenado em cache. Por exemplo, os cabeçalhos Cache-Control: private, Cache-Control: no-cache ou Pragma: no-cache impedirão que um arquivo seja armazenado em cache.
* Solicitações de intervalo de bytes para conteúdo parcialmente armazenado em cache.

Olá fórmula é: (TCP_ ACERTOS / (TCP_ ocorrências + TCP_MISS)) * 100

* Selecionar dados de tooview de intervalo de data de hoje/esta semana/mês, etc. ou inserir datas personalizadas, clique em "Ir" toomake se que a seleção está atualizada.
* Você pode exportar e baixar dados de saudação clicando Olá localizado ao lado do ícone de planilha do excel muito "Ir".

![Relatório Taxa de acertos do cache](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>Dados IPv4/IPV6 Transferidos
Este relatório mostra a distribuição de uso de tráfego Olá no vs IPV4 IPV6.

![Dados IPv4/IPV6 Transferidos](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Selecionar dados de tooview de intervalo de data de hoje/esta semana/mês, etc., ou insira datas personalizadas.
* Clique em "Ir" toomake se que a seleção está atualizada.

## <a name="considerations"></a>Considerações
Relatórios só podem ser gerados no hello últimos 18 meses.

