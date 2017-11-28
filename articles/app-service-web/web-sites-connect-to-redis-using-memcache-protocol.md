---
title: "aaaConnect um tooRedis de aplicativo do serviço de aplicativo web via Olá protocolo Memcache - Azure | Microsoft Docs"
description: "Conecte-se um aplicativo web no serviço de aplicativo do Azure tooRedis Cache usando o protocolo Memcache de saudação"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Conecte-se um aplicativo web no serviço de aplicativo do Azure tooRedis Cache por meio do protocolo Memcache de saudação
Neste artigo, você aprenderá como tooconnect um WordPress web app [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) muito[Cache Redis do Azure] [ 12] usando Olá [Memcache] [ 13] protocolo. Se você tiver um aplicativo web existente que usa um servidor de Memcached para cache na memória, você pode migrá-lo tooAzure do serviço de aplicativo e use Olá primários solução de cache no Microsoft Azure com pouca ou nenhuma alteração tooyour código do aplicativo. Além disso, você pode usar os Memcache experiência toocreate altamente escalonáveis e distribuídos aplicativos existentes no serviço de aplicativo do Azure com o Cache Redis do Azure para o cache na memória, durante o uso de estruturas de aplicativos populares, como .NET, PHP, Node.js, Java e Python.  

Os aplicativos do serviço de aplicativo Web permite que esse cenário de aplicativo com a correção de Memcache de aplicativos Web hello, que é um servidor local Memcached que atua como um proxy de Memcache para armazenar em cache chamadas tooAzure Cache Redis. Isso permite que qualquer aplicativo que se comunica usando dados de toocache Olá Memcache protocolo com Cache Redis. Essa correção de Memcache funciona no nível de protocolo hello, portanto ele pode ser usado por qualquer aplicativo ou a estrutura de aplicativo desde que ele se comunica usando o protocolo Memcache de saudação.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Pré-requisitos
correção de Memcache de aplicativos Web Hello pode ser usada com qualquer aplicativo desde que ele se comunica usando o protocolo Memcache de saudação. Para esse exemplo específico, o aplicativo de referência de saudação é um site de WordPress escalonável que pode ser provisionado de saudação do Azure Marketplace.

Execute as etapas de saudação descritas neste artigo:

* [Provisionar uma instância do hello serviço de Cache Redis do Azure][0]
* [Implantar um site do WordPress escalonável no Azure][1]

Uma vez que o site de WordPress escalonável Olá implantados e uma instância de Redis Cache provisionado será tooproceed pronto com a habilitação de correção de Memcache Olá em aplicativos de Web do serviço de aplicativo do Azure.

## Permitir correção de Memcache de aplicativos Web Olá
Correção de Memcache de tooconfigure de ordem, você deve criar três configurações de aplicativo. Isso pode ser feito usando uma variedade de métodos, incluindo Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715), Olá [portal clássico][3], Olá [Cmdlets do PowerShell do Azure] [ 5] ou hello [Interface de linha de comando do Azure][5]. Para fins de saudação esta postagem, vou Olá toouse [Portal do Azure] [ 4] configurações do aplicativo hello tooset. Olá valores a seguir podem ser recuperados de **configurações** folha da sua instância de Cache Redis.

![Folha de configurações de Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### Adicionar configurações de aplicativo REDIS_HOST
Olá primeira configuração de aplicativo, você precisa toocreate é hello **REDIS\_HOST** configuração do aplicativo. Esta configuração define Olá toowhich Olá shim encaminhamentos Olá cache informações de destino. Olá valor necessário para a configuração do aplicativo hello REDIS_HOST pode ser recuperada da saudação **propriedades** folha da sua instância de Cache Redis.

![Nome do Host do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Conjunto Olá chave de configuração de aplicativo de saudação muito**REDIS\_HOST** e o valor de saudação do toohello de configuração de aplicativo hello **hostname** da instância de Cache Redis hello.

![REDIS_HOST de AppSetting Aplicativo Web ](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### Adicionar a configuração de aplicativo REDIS_KEY
Olá segunda configuração de aplicativo, você precisa toocreate é hello **REDIS\_chave** configuração do aplicativo. Essa configuração fornece uma instância de Cache Redis Olá autenticação token toosecurely necessário acesso hello. Você pode recuperar o valor de saudação necessária para configuração de aplicativo REDIS_KEY saudação do hello **chaves de acesso** folha da instância de Cache Redis hello.

![Chave primária do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Conjunto Olá chave de configuração de aplicativo de saudação muito**REDIS\_chave** e o valor de saudação do toohello de configuração de aplicativo hello **chave primária** da instância de Cache Redis hello.

![REDIS_KEY AppSetting de Site do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### Adicionar a configuração de aplicativo MEMCACHESHIM_REDIS_ENABLE
última configuração de aplicativo Hello é usado tooenable Olá Memcache Shim em aplicativos da Web, que usa Olá REDIS_HOST e REDIS_KEY tooconnect toohello Cache Redis do Azure e Olá encaminhar chamadas de cache. Chave de saudação de conjunto de configuração de aplicativo de saudação muito**MEMCACHESHIM\_REDIS\_habilitar** e Olá valor muito**true**.

![MEMCACHESHIM_REDIS_ENABLE de AppSetting de Aplicativo Web](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Quando você terminar de adicionar configurações de aplicativo hello três (3), clique em **salvar**.

## Habilitar a extensão de Memcache para PHP
Em ordem para Olá toospeak de aplicativo hello protocolo Memcache, é tooPHP de extensão do tooinstall necessário Olá Memcache - estrutura de linguagem Olá para seu site de WordPress.

### Baixar Olá php_memcache extensão
Procurar muito[PECL][6]. Em Olá cache categoria, clique em [memcache][7]. Na coluna de downloads de saudação clique o link DLL de saudação.

![Site PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Link de Thread não seguro (NTES) x86 Olá para a versão de saudação do PHP habilitado em aplicativos da Web de download. (O padrão é PHP 5.4)

![Pacote de Memcache do site PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Habilitar a extensão de php_memcache Olá
Depois de baixar o arquivo hello, descompacte e carregar Olá **php\_memcache.dll** em Olá **unidade d:\\inicial\\site\\wwwroot\\bin\\ext\\**  directory. Depois de php_memcache.dll Olá carregada no aplicativo web de Olá, é necessário tooenable Olá extensão toohello tempo de execução do PHP. Olá tooenable Memcache extensão em Olá Portal do Azure, abra Olá **configurações do aplicativo** folha de aplicativo da web hello, adicione uma nova configuração de aplicativo com a chave de saudação do **PHP\_extensões** e hello valor **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Se precisar de aplicativo da web de saudação tooload várias extensões PHP, valor de saudação do PHP_EXTENSIONS deve ser uma lista delimitada por vírgulas de arquivos de tooDLL caminhos relativos.
> 
> 

![PHP_EXTENSIONS de AppSetting de Aplicativo Web](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

Ao terminar, clique em **Salvar**.

## Instalar o plug-in do WordPress do Memcache
> [!NOTE]
> Você também pode baixar Olá [plug-in de Cache de objeto Memcached](https://wordpress.org/plugins/memcached/) de WordPress.org.
> 
> 

Na página de plug-ins do WordPress hello, clique em **adicionar novo**.

![Página de plug-in do WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Na caixa de pesquisa hello, digite **memcached** e pressione **Enter**.

![Adicionar novo plug-in do WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Localizar **Memcached objeto Cache** na lista de hello, em seguida, clique em **instalar agora**.

![Instalar o plug-in Memcache do WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Habilitar Olá plug-in do Memcache WordPress
> [!NOTE]
> Siga as instruções de saudação neste blog [como uma extensão de Site em aplicativos da Web de tooenable] [ 8] tooinstall do Visual Studio Team Services.
> 
> 

Em Olá `wp-config.php` de arquivo, adicione Olá seguindo o código acima comentário de edição de parada Olá final de saudação do arquivo hello.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Depois que esse código foi colado, monaco salvará automaticamente documento hello.

Olá próxima etapa é o plug-in de cache de objetos de saudação tooenable. Isso é feito arrastando e soltando **cache.php objeto** de **wp-conteúdo/plug-ins/memcached** pasta toohello **wp conteúdo** tooenable pasta Olá Memcache objeto Funcionalidade de cache.

![Localize o plug-in do hello memcache cache.php de objeto](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Agora que Olá **objeto cache.php** arquivo está no hello **wp conteúdo** pasta, Olá Memcached objeto de Cache está ativado.

![Habilitar o plug-in do hello memcache cache.php de objeto](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Verifique se Olá Memcache objeto Cache plug-in está funcionando
Todos os Olá etapas tooenable Olá Web Apps Memcache shim agora estão completos. Olá só resta tooverify que dados saudação é preencher sua instância de Cache Redis.

### Habilitar o suporte de porta não SSL Olá no Cache Redis do Azure
> [!NOTE]
> Em tempo de saudação de escrever este artigo, Olá Redis CLI não oferece suporte a conectividade SSL, assim hello etapas a seguir são necessárias.
> 
> 

No Portal do Azure do hello, procure instância de Cache Redis toohello que você criou para este aplicativo web. Depois de folha do cache Olá estiver aberta, clique em Olá **configurações** ícone.

![Botão de configurações de Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Selecione **portas de acesso** da lista de saudação.

![Porta de acesso do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Clique em **Não** para **Permitir acesso somente via SSL**.

![Porta de acesso somente SSL do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Você verá que a porta de não-SSL Olá agora está definida. Clique em **Salvar**.

![Acessar o Portal não SSL do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Conectar tooAzure Cache Redis do redis-cli
> [!NOTE]
> Essa etapa pressupõe que o Redis esteja instalado localmente em seu computador de desenvolvimento. [Instale o Redis localmente usando estas instruções][9].
> 
> 

Abra o console de linha de comando de saudação escolha e o tipo de comando a seguir:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Substituir saudação  **&lt;nome de host para o cache redis&gt;**  com hello xxxxx.redis.cache.windows.net real hostname e hello  **&lt;primária-chave-para--cache redis&gt;**  com chave de acesso de saudação do cache hello, pressione **Enter**. Quando hello CLI conectou instância de Cache Redis toohello, emita um comando redis. Abaixo da captura de tela hello, escolhi toolist chaves hello.

![Conectar tooAzure Cache Redis do Redis CLI no Terminal](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

chaves de Olá Olá chamada toolist devem retornar um valor. Caso contrário, tente navegar toohello web app e tente novamente.

## Conclusão
Parabéns! Olá WordPress aplicativo agora tem um tooaid centralizado no cache na memória aumentar a taxa de transferência. Lembre-se, Olá correção de Memcache de aplicativos Web podem ser usada com qualquer cliente Memcache, independentemente da estrutura de aplicativo ou linguagem de programação. comentários ou tooask perguntas sobre correção de Memcache de aplicativos Web hello, tooprovide lançar muito[fóruns MSDN] [ 10] ou [Stackoverflow][11].

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto em serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
