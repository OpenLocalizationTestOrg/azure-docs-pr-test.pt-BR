---
title: "aaaAdd tooan um CDN do serviço de aplicativo do Azure | Microsoft Docs"
description: "Adicionar um toocache de serviço de aplicativo do Azure Content Delivery Network (CDN) tooan e entregar seus arquivos estáticos de servidores clientes tooyour Fechar ao redor Olá, mundo."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>Adicionar uma tooan de rede de fornecimento de conteúdo (CDN) do serviço de aplicativo do Azure

[Rede de fornecimento de conteúdo do Azure (CDN)](../cdn/cdn-overview.md) armazena em cache o conteúdo estático da web em locais estrategicamente colocados tooprovide taxa de transferência máxima para entregar conteúdo toousers. Olá CDN também reduz a carga do servidor em seu aplicativo web. Este tutorial mostra como tooadd Azure CDN tooa [aplicativo web no serviço de aplicativo do Azure](app-service-web-overview.md). 

Aqui está o hello home page do hello exemplo site HTML estático que você trabalhará com:

![Home page do aplicativo de exemplo](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

O que você aprenderá:

> [!div class="checklist"]
> * Criar um novo ponto de extremidade do CDN.
> * Atualizar ativos em cache.
> * Usar consulta de cadeias de caracteres versões toocontrol armazenado em cache.
> * Use um domínio personalizado para o ponto de extremidade CDN hello.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

- [Instalar o Git](https://git-scm.com/)
- [Instalar a CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Criar aplicativo web de saudação

aplicativo web do toocreate Olá que você trabalhará com hello siga [início rápido HTML estático](app-service-web-get-started-html.md) por meio de saudação **procurar toohello aplicativo** etapa.

### <a name="have-a-custom-domain-ready"></a>Tenha um domínio personalizado pronto

etapa de domínio personalizado Olá toocomplete deste tutorial, você precisa tooown um domínio personalizado e ter acessar tooyour o registro DNS para o seu provedor de domínio (como GoDaddy). Por exemplo, as entradas DNS tooadd para `contoso.com` e `www.contoso.com`, você deve ter acesso tooconfigure Olá as configurações de DNS para Olá `contoso.com` domínio raiz.

Se você ainda não tiver um nome de domínio, considere a seguir Olá [tutorial de domínio do serviço de aplicativo](custom-dns-web-site-buydomains-web-app.md) toopurchase usando um domínio Olá portal do Azure. 

## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure

Abra um navegador e navegue toohello [portal do Azure](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>Como criar um perfil do CDN e um ponto de extremidade

No hello barra de navegação esquerda, selecione **serviços de aplicativos**e em seguida, selecione o aplicativo hello que você criou no hello [início rápido HTML estático](app-service-web-get-started-html.md).

![Selecione o aplicativo de serviço de aplicativo no portal de saudação](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

Em Olá **do serviço de aplicativo** página Olá **configurações** seção, selecione **rede > configurar o Azure CDN para seu aplicativo**.

![Selecione a CDN no portal de saudação](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

Em Olá **rede de fornecimento de conteúdo do Azure** , forneça Olá **novo ponto de extremidade** configurações conforme especificado na tabela de saudação.

![Criar perfil e o ponto de extremidade no portal de saudação](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Configuração | Valor sugerido | Descrição |
| ------- | --------------- | ----------- |
| **Perfil do CDN** | myCDNProfile | Selecione **criar novo** toocreate perfil CDN. Perfil CDN é uma coleção de pontos de extremidade CDN com hello mesma camada de preços. |
| **Tipo de preços** | Akamai Standard | Olá [preço](../cdn/cdn-overview.md#azure-cdn-features) Especifica o provedor de saudação e recursos disponíveis. Neste tutorial, estamos usando o Akamai padrão. |
| **Nome do ponto de extremidade do CDN** | Qualquer nome que seja exclusivo no domínio de azureedge.net Olá | Acessar os recursos armazenados em cache no domínio Olá  *\<endpointname >. azureedge.net*.

Selecione **Criar**.

O Azure cria o ponto de extremidade e perfil de saudação. novo ponto de extremidade de saudação aparece no hello **pontos de extremidade** lista Olá a mesma página, e quando ela é provisionada status Olá é **executando**.

![Ponto de extremidade novo na lista](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Saudação de teste ponto de extremidade CDN

Se você selecionou o tipo de preços da Verizon, normalmente demora cerca de 90 minutos para a propagação de ponto de extremidade. Para Akamai, leva alguns minutos para ocorrer a propagação

aplicativo de exemplo Hello tem um `index.html` arquivo e *css*, *img*, e *js* pastas que contêm outros ativos estáticos. Olá conteúdo de caminhos para todos esses arquivos são Olá mesmo ponto de extremidade de CDN hello. Por exemplo, ambos Olá seguintes URLs acessam Olá *bootstrap.css* arquivo hello *css* pasta:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Navegue até um toohello de navegador a URL a seguir:

```
http://<endpointname>.azureedge.net/index.html
```

![Home page do aplicativo de exemplo distribuídos a partir do CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Você verá Olá mesma página que você executou anteriormente em um aplicativo web do Azure. CDN do Azure recuperou ativos do aplicativo de web para a origem hello e está servindo-los do ponto de extremidade CDN Olá

tooensure que esta página é armazenada em cache no hello CDN, página de atualização de saudação. Duas solicitações para hello mesmo ativo às vezes são necessárias para CDN toocache Olá Olá conteúdo solicitado.

Para obter mais informações sobre como criar perfis do CDN do Azure e pontos de extremidade, confira [Introdução ao CDN do Azure](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Limpar Olá CDN

Olá CDN atualiza periodicamente seus recursos do aplicativo de web de origem Olá com base na configuração do hello time-to-live (TTL). TTL padrão de saudação é de sete dias.

Às vezes pode ser necessário toorefresh Olá CDN antes Olá expiração do tempo de vida – por exemplo, quando você implanta o aplicativo da web de toohello conteúdo atualizado. tootrigger uma atualização, você pode limpar manualmente recursos CDN hello. 

Nesta seção do tutorial hello, implantar um aplicativo da web toohello alteração e limpar Olá CDN tootrigger Olá CDN toorefresh seu cache.

### <a name="deploy-a-change-toohello-web-app"></a>Implantar um aplicativo de web de toohello de alteração

Olá abra `index.html` e adicione "-V2" toohello H1 título, conforme mostrado no exemplo a seguir de saudação: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Confirmar suas alterações e implantá-lo toohello web app.

```bash
git commit -am "version 2"
git push azure master
```

Depois que a implantação for concluída, a URL de aplicativo de web toohello procurar e você verá Olá alterar.

```
http://<appname>.azurewebsites.net/index.html
```

![V2 no título no aplicativo web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

Procurar toohello URL de ponto de extremidade CDN para a home page do hello e você não vir Olá alterar porque a versão armazenada em cache Olá no hello CDN ainda não expirou. 

```
http://<endpointname>.azureedge.net/index.html
```

![Nenhum V2 no título no CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Limpar Olá CDN no portal de saudação

tootrigger Olá CDN tooupdate sua versão armazenada em cache, limpe Olá CDN.

No hello portal de navegação esquerdo, selecione **grupos de recursos**e, em seguida, selecione o grupo de recursos de saudação que você criou para seu aplicativo web (myResourceGroup).

![Escolha o grupo de recursos](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

Na lista de saudação de recursos, selecione o ponto de extremidade CDN.

![Selecione o ponto de extremidade](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

Na parte superior de saudação do hello **ponto de extremidade** , clique em **limpar**.

![Selecione Limpar](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Insira os caminhos de conteúdo Olá desejar toopurge. Você pode passar um toopurge de caminho de arquivo completo de um arquivo individual ou um toopurge de segmento de caminho e atualizar todo o conteúdo em uma pasta. Como você alterou `index.html`, certifique-se de que é um dos caminhos de saudação.

Final Olá Olá página, selecione **limpar**.

![Limpar página](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>Verifique se esse Olá que CDN é atualizada

Aguarde até que a solicitação de limpeza Olá termina de processar, normalmente de alguns minutos. toosee Olá o status atual, ícone de sino Olá select na parte superior de saudação da página de saudação. 

![Limpar notificação](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Procurar toohello URL de ponto de extremidade CDN para `index.html`, e agora você verá Olá V2 que você adicionou toohello título na home page do hello. Isso mostra que o cache CDN Olá foi atualizada.

```
http://<endpointname>.azureedge.net/index.html
```

![V2 no título no CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Para obter mais informações, confira [Como limpar um ponto de extremidade do CDN do Azure](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Usar o conteúdo de tooversion de cadeias de caracteres de consulta

Olá CDN do Azure oferece Olá cache comportamento as opções a seguir:

* Ignorar as cadeias de caracteres de consulta
* Ignorar o cache para cadeias de caracteres de consulta
* Armazenar em cache todas as URLs exclusivas 

Olá primeiro deles é padrão hello, o que significa que há somente uma versão em cache de um ativo, independentemente da cadeia de caracteres de consulta de Olá Olá URL. 

Nesta seção do tutorial hello, você alterar Olá cache comportamento toocache todas as URLs exclusivas.

### <a name="change-hello-cache-behavior"></a>Alterar o comportamento do cache Olá

No portal do Azure de saudação **ponto de extremidade CDN** página, selecione **Cache**.

Selecione **armazenar em Cache todas as URLs exclusivas** de saudação **comportamento do cache de cadeia de consulta** lista suspensa.

Selecione **Salvar**.

![Selecione o comportamento do armazenamento em cache da cadeia de caracteres de consulta](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Verifique se as URLs exclusivas são armazenadas em cache separadamente

Em um navegador, navegue toohello home page no ponto de extremidade CDN hello, mas incluir uma cadeia de caracteres de consulta: 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

Olá CDN retorna Olá atual conteúdo da web app, que inclui "V2" no título da saudação. 

tooensure que esta página é armazenada em cache no hello CDN, página de atualização de saudação. 

Abra `index.html` e alterar "V2" muito "V3" e implantar a alteração de saudação. 

```bash
git commit -am "version 3"
git push azure master
```

Em um navegador, vá toohello URL de ponto de extremidade CDN com uma nova cadeia de caracteres de consulta, como `q=2`. Olá CDN obtém Olá atual `index.html` de arquivos e exibe "V3".  Porém, se você navegar toohello o ponto de extremidade CDN com hello `q=1` cadeia de caracteres, consulte "V2".

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 no título no CDN, cadeia de caracteres de consulta 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 no título no CDN, cadeia de caracteres de consulta 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

A saída mostra que cada cadeia de caracteres de consulta é tratada de maneira diferente:

* p = 1 foi usada antes e, portanto, o conteúdo em cache é retornado (V2).
* p = 2 é novo, portanto, conteúdo de aplicativo da web mais recente Olá é recuperado e retornado (V3).

Para obter mais informações, confira [controle do comportamento do armazenamento em cache do CDN do Azure com cadeias de caracteres de consulta](../cdn/cdn-query-string.md).

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Mapear um ponto de extremidade CDN do domínio personalizado tooa

Criando um registro CNAME, você vai mapear seu domínio personalizado de tooyour ponto de extremidade CDN. Um registro CNAME é um recurso DNS que mapeia um domínio de destino de tooa de domínio de origem. Por exemplo, você pode mapear `cdn.contoso.com` ou `static.contoso.com` muito`contoso.azureedge.net`.

Se você não tiver um domínio personalizado, considere a seguir Olá [tutorial de domínio do serviço de aplicativo](custom-dns-web-site-buydomains-web-app.md) toopurchase usando um domínio Olá portal do Azure. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Localizar Olá hostname toouse com hello CNAME

No portal do Azure de saudação **ponto de extremidade** página, certifique-se de **visão geral** está selecionado na saudação à esquerda de navegação e, em seguida, selecione hello **+ domínio personalizado** botão na parte superior de saudação da página de saudação.

![Selecione Adicionar domínio personalizado](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

Em Olá **adicionar um domínio personalizado** página, você verá toouse de nome de host Olá ponto de extremidade na criação de um registro CNAME. nome de host de saudação é derivado da sua URL de ponto de extremidade CDN:  **&lt;EndpointName >. azureedge.net**. 

![Adicionar página de domínio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Configurar Olá CNAME com seu registrador de domínio

Navegue de site do registrador de domínio tooyour e localize a seção Olá para criar registros DNS. Você pode encontrá-lo em uma seção como **Nome de Domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.

Localize seção Olá para gerenciar CNAMEs. Você pode ter a página de configurações avançadas de tooan toogo e procure palavras Olá CNAME, Alias ou subdomínios.

Criar um registro CNAME que mapeie o subdomínio escolhido (por exemplo, **estático** ou **cdn**) toohello **nome de host do ponto de extremidade** mostrado anteriormente no portal de saudação. 

### <a name="enter-hello-custom-domain-in-azure"></a>Digite o domínio personalizado Olá no Azure

Retornar toohello **adicionar um domínio personalizado** página e, em seguida, digite seu domínio personalizado, incluindo o subdomínio hello, na caixa de diálogo de saudação. Por exemplo, insira: `cdn.contoso.com`.   
   
Azure verifica se o registro CNAME Olá existe para nome de domínio Olá que você inseriu. Se Olá CNAME estiver correto, seu domínio personalizado será validado.

Pode levar tempo para Olá CNAME toopropagate registro tooname servidores em Olá Internet. Se o domínio não for validado imediatamente, aguarde alguns minutos e tente novamente.

### <a name="test-hello-custom-domain"></a>Domínio personalizado de saudação de teste

Em um navegador, navegue toohello `index.html` arquivo usando seu domínio personalizado (por exemplo, `cdn.contoso.com/index.html`) tooverify é resultado de Olá Olá mesmo como quando você entrar diretamente muito`<endpointname>azureedge.net/index.html`.

![Home page do aplicativo de exemplo usando a URL do domínio personalizado](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Para obter mais informações, consulte [domínio personalizado do mapa do Azure CDN tooa conteúdo](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Próximas etapas

O que você aprendeu:

> [!div class="checklist"]
> * Criar um novo ponto de extremidade do CDN.
> * Atualizar ativos em cache.
> * Usar consulta de cadeias de caracteres versões toocontrol armazenado em cache.
> * Use um domínio personalizado para o ponto de extremidade CDN hello.

Saiba como toooptimize desempenho CDN Olá seguintes artigos:

> [!div class="nextstepaction"]
> [Melhorar o desempenho compactando os arquivos na CDN do Azure](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Pré-carregar ativos em um ponto de extremidade da CDN do Azure](../cdn/cdn-preload-endpoint.md)
