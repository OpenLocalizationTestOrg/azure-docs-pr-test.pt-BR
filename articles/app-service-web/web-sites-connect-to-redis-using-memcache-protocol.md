---
title: "Conectar um aplicativo Web no Serviço de Aplicativo ao Redis por meio do protocolo Memcache - Azure | Microsoft Docs"
description: "Conectar um aplicativo Web no Serviço de Aplicativo do Azure ao Cache Redis por meio do protocolo Memcache"
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
ms.openlocfilehash: 0eea1d64a50bec8fb7da155e2088ddfc36b377f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# Conectar um aplicativo Web no Serviço de Aplicativo do Azure ao Cache Redis por meio do protocolo Memcache
Neste artigo, você verá como conectar um aplicativo Web do WordPress no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) ao [CAche Redis do Azure][12] usando o protocolo [Memcache][13]. Se tiver um aplicativo Web existente que usa um servidor Memcached para cache na memória, você poderá migrá-lo para o Serviço de Aplicativo do Azure e usar a solução de cache de terceiros no Microsoft Azure com pouca ou nenhuma alteração no código do aplicativo. Além disso, você pode usar sua experiência com o Memcache para criar aplicativos distribuídos altamente escalonáveis no Serviço de Aplicativo do Azure com o Cache Redis do Azure para cache em memória, usando estruturas de aplicativos populares, como .NET, PHP, Node.js, Java e Python.  

Os aplicativos Web do Serviço de Aplicativo habilitam esse cenário de aplicativo com o shim do Memcache de aplicativos Web, que é um servidor Memcached local que atua como um proxy Memcache para armazenar em cache as chamadas ao Cache Redis do Azure. Isso habilita qualquer aplicativo que se comunica usando o protocolo Memcache a armazenar dados em cache com o Cache Redis. Esse shim do Memcache funciona no nível do protocolo; portanto, ele pode ser usado por qualquer aplicativo ou estrutura de aplicativo, desde que se comunique usando o protocolo Memcache.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Pré-requisitos
O shim do Memcache de aplicativos Web pode ser usado com qualquer aplicativo, desde que se comunique usando o protocolo Memcache. Para este exemplo específico, o aplicativo de referência é um site do WordPress escalonável que pode ser provisionado do Azure Marketplace.

Siga as etapas descritas nestes artigos:

* [Provisionar uma instância do Serviço de Cache Redis do Azure][0]
* [Implantar um site do WordPress escalonável no Azure][1]

Depois que o site do WordPress escalonável for implantado e uma instância do Cache Redis for provisionada, você estará pronto para prosseguir com a habilitação do shim do Memcache em aplicativos Web do Serviço de Aplicativo do Azure.

## Habilitar o shim do Memcache de aplicativos Web
Para configurar o shim do Memcache, você deve criar três configurações de aplicativo. Isso pode ser feito usando diversos métodos, incluindo o [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715), o [portal clássico][3], os [Cmdlets do Azure PowerShell][5] ou a [Interface de Linha de Comando do Azure][5]. Para os fins desta postagem, vou usar o [Portal do Azure][4] para definir as configurações do aplicativo. Os valores a seguir podem ser recuperados da folha **Configurações** de sua instância do Cache Redis.

![Folha de configurações de Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### Adicionar configurações de aplicativo REDIS_HOST
A primeira configuração de aplicativo que você precisa criar é **REDIS\_HOST**. Essa configuração define o destino para o qual o shim encaminha as informações de cache. O valor necessário para a configuração de aplicativo REDIS_HOST pode ser recuperado da folha **Propriedades** de sua instância do Cache Redis.

![Nome do Host do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Defina a chave da configuração de aplicativo como **REDIS\_HOST** e o valor da configuração de aplicativo como o **hostname** da instância do Cache Redis.

![REDIS_HOST de AppSetting Aplicativo Web ](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### Adicionar a configuração de aplicativo REDIS_KEY
A segunda configuração de aplicativo que você precisa criar é **REDIS\_KEY**. Essa configuração fornece o token de autenticação necessário para acessar com segurança a instância do Cache Redis. Você pode recuperar o valor necessário para a configuração de aplicativo REDIS_KEY na folha **Chaves de acesso** da instância do Cache Redis.

![Chave primária do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Defina a chave da configuração de aplicativo como **REDIS\_KEY** e o valor da configuração de aplicativo como a **Chave Primária** da instância do Cache Redis.

![REDIS_KEY AppSetting de Site do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### Adicionar a configuração de aplicativo MEMCACHESHIM_REDIS_ENABLE
A última configuração de aplicativo é usada para habilitar a correção do Memcache em aplicativos Web, que usa REDIS_HOST e REDIS_KEY para se conectar ao Cache Redis do Azure e encaminhar as chamadas de cache. Defina a chave da configuração de aplicativo como **MEMCACHESHIM\_REDIS\_ENABLE** e o valor como **true**.

![MEMCACHESHIM_REDIS_ENABLE de AppSetting de Aplicativo Web](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Após adicionar as três (3) configurações de aplicativo, clique em **Salvar**.

## Habilitar a extensão de Memcache para PHP
Para que o aplicativo fale com o protocolo Memcache, é necessário instalar a extensão Memcache para PHP (a estrutura de linguagem para seu site do WordPress).

### Baixar a extensão php_memcache
Navegue até [PECL][6]. Na categoria de cache, clique em [memcache][7]. Na coluna de downloads, clique no link DLL.

![Site PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Baixe o link x86 NTS (Non-Thread Safe) para a versão do PHP habilitada nos aplicativos Web. (O padrão é PHP 5.4)

![Pacote de Memcache do site PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Habilitar a extensão php_memcache
Depois de baixar o arquivo, descompacte e carregue **php\_memcache.dll** no diretório **d:\\home\\site\\wwwroot\\bin\\ext\\**. Depois que o php_memcache.dll for carregado no aplicativo Web, você precisará habilitar a extensão no Tempo de Execução do PHP. Para habilitar a extensão Memcache no Portal do Azure, abra a folha **Configurações de Aplicativo** do aplicativo Web e adicione uma nova configuração de aplicativo com a chave de **PHP\_EXTENSIONS** e o valor **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Se o aplicativo Web precisar carregar várias extensões PHP, o valor de PHP_EXTENSIONS deverá ser uma lista delimitada por vírgulas de caminhos relativos para arquivos DLL.
> 
> 

![PHP_EXTENSIONS de AppSetting de Aplicativo Web](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

Ao terminar, clique em **Salvar**.

## Instalar o plug-in do WordPress do Memcache
> [!NOTE]
> Você também pode baixar o [Plug-in de Cache do Objeto Memcached](https://wordpress.org/plugins/memcached/) em WordPress.org.
> 
> 

Na página de plug-ins do WordPress, clique em **Adicionar Novo**.

![Página de plug-in do WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Na caixa de pesquisa, digite **memcached** e pressione **Enter**.

![Adicionar novo plug-in do WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Localize **Cache de Objeto Memcached** na lista e clique em **Instalar Agora**.

![Instalar o plug-in Memcache do WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Habilitar o plug-in do WordPress do Memcache
> [!NOTE]
> Siga as instruções neste blog sobre [Como habilitar uma Extensão de Site em Aplicativos Web][8] para instalar o Visual Studio Team Services.
> 
> 

No arquivo `wp-config.php` , adicione o código a seguir acima do comentário de interrupção de edição próximo ao fim do arquivo.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Depois que esse código for colado, monaco salvará automaticamente o documento.

A próxima etapa é habilitar o plug-in object-cache. Para isso, arraste e solte **object-cache.php** da pasta **wp-content/plugins/memcached** para a pasta **wp-content** para habilitar a funcionalidade cache de objetos do Memcache.

![Localizar o plug-in memcache object-cache.php](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Agora que o arquivo **object-cache.php**p está na pasta **wp-content**, o cache de objetos Memcached agora está habilitado.

![Habilitar o plug-in memcache object-cache.php](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Verificando se o plug-in de cache de objetos do Memcache está funcionando
Todas as etapas para habilitar o shim do Memcache de aplicativos Web foram concluídas. Só resta verificar se os dados estão populando sua instância do Cache Redis.

### Habilitar o suporte à porta não SSL no Cache Redis do Azure
> [!NOTE]
> Quando este artigo foi escrito, a CLI do Redis não dava suporte à conectividade SSL; portanto, as etapas a seguir são necessárias.
> 
> 

No Portal do Azure, navegue até a instância do Cache Redis que você criou para o aplicativo Web. Quando a folha do cache for aberta, clique no ícone **Configurações** .

![Botão de configurações de Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Selecione **Portas de Acesso** na lista.

![Porta de acesso do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Clique em **Não** para **Permitir acesso somente via SSL**.

![Porta de acesso somente SSL do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Você verá que a porta não SSL agora está definida. Clique em **Salvar**.

![Acessar o Portal não SSL do Cache Redis do Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Conectar ao Cache Redis do Azure por meio de redis-cli
> [!NOTE]
> Essa etapa pressupõe que o Redis esteja instalado localmente em seu computador de desenvolvimento. [Instale o Redis localmente usando estas instruções][9].
> 
> 

Abra o console de linha de comando de sua escolha e digite o seguinte comando:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Substitua **&lt;nomedohost-para-cache-redis&gt;** pelo nome do host real xxxxx.redis.cache.windows.net e **&lt;primary-key-for-redis-cache&gt;** pela chave de acesso para o cache e pressione **Enter**. Depois que a CLI for conectada à instância do Cache Redis, execute qualquer comando do Redis. Na captura de tela abaixo, optei por listar as chaves.

![Conectar ao Cache Redis do Azure por meio de Redis CLI no Terminal](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

A chamada para listar as chaves deve retornar um valor. Caso contrário, tente navegar até o aplicativo Web e tente novamente.

## Conclusão
Parabéns! O aplicativo do WordPress agora tem um cache na memória centralizado para ajudar a aumentar a taxa de transferência. Lembre-se: o shim do Memcache de aplicativos Web pode ser usado com qualquer cliente Memcache, independentemente da linguagem de programação ou da estrutura de aplicativo. Para fornecer comentários ou fazer perguntas sobre o shim do Memcache de aplicativos Web, poste nos [Fóruns do MSDN][10] ou no[Stackoverflow][11].

> [!NOTE]
> Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## O que mudou
* Para obter um guia sobre a alteração de sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

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
