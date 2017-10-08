---
title: ambientes de DevOps aaaUse efetivamente para seu aplicativo web | Microsoft Docs
description: "Saiba como toouse slots da implantação tooset backup e gerenciar vários ambientes de desenvolvimento para seu aplicativo"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Usar ambientes de Operações de Desenvolvimento com eficiência em seus aplicativos Web
Este artigo mostra como tooset e gerenciar implantações de aplicativo web quando várias versões do seu aplicativo em vários ambientes, como desenvolvimento, teste, qualidade (QA) e produção. Cada versão do seu aplicativo pode ser considerado como um ambiente de desenvolvimento para finalidade específica de saudação do processo de implantação. Por exemplo, os desenvolvedores podem usar Olá qualidade do controle de qualidade ambiente tootest saudação do aplicativo hello antes de eles push Olá alterações tooproduction.
Vários ambientes de desenvolvimento podem ser um desafio porque você precisa de código tootrack, gerenciar recursos (computação, aplicativo web, banco de dados, cache, etc.) e implante o código em ambientes.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Configurar um ambiente de não produção (estágio, desenvolvimento, controle de qualidade)
Depois que um aplicativo da web de produção estiver em execução, Olá próxima etapa é toocreate um ambiente de não produção. toouse slots de implantação, certifique-se de que você está executando no modo de plano Standard ou o serviço de aplicativo do Azure Premium Olá. Os slots de implantação são aplicativos Web dinâmicos com seus próprios nomes de host. Elementos de conteúdo e configuração de aplicativo da Web podem ser trocados entre os dois slots de implantação, incluindo o slot de produção de hello. Quando você implanta o slot de implantação do aplicativo tooa, você obtém Olá benefícios a seguir:

- Você pode validar o aplicativo de web tooa alterações em um slot de implantação de preparo antes de alternar o aplicativo hello com o slot de produção de hello.
- Quando você implanta um slot de tooa do aplicativo web primeiro e troque-o em produção, todas as instâncias do slot de saudação são aquecidas antes de ser trocadas em produção. Esse processo elimina o tempo de inatividade quando você for implantar seu aplicativo Web. Olá redirecionamento do tráfego é contínuo e nenhuma solicitação é descartada devido a operações de tooswap. tooautomate esse fluxo de trabalho inteiro, configurar [troca automática](web-sites-staged-publishing.md#configure-auto-swap) quando a validação de pré-permuta não é necessária.
- Após uma troca slot Olá que tem o aplicativo web de saudação preparado anteriormente agora tem Olá aplicativo de web de produção anterior. Se alterações Olá trocadas no slot de produção de hello estiverem não conforme o esperado, você pode executar Olá mesma troca imediatamente tooget seu "última boas" back do aplicativo web.

tooset backup de um slot de implantação de preparo, consulte [configurar ambientes de preparo para aplicativos web no serviço de aplicativo do Azure](web-sites-staged-publishing.md). Cada ambiente deve incluir seu próprio conjunto de recursos. Por exemplo, se o seu aplicativo Web usar um banco de dados, os aplicativos Web de preparo e produção deverão usar bancos de dados diferentes. Adicione seu ambiente de desenvolvimento de preparo de preparo recursos do ambiente de desenvolvimento como tooset de cache, armazenamento ou banco de dados.

## <a name="examples-of-using-multiple-development-environments"></a>Exemplos de uso de vários ambientes de desenvolvimento
Qualquer projeto deve seguir o gerenciamento de código fonte com pelo menos dois ambientes: desenvolvimento e produção. Se você usar sistemas de gerenciamento de conteúdo (CMSs), estruturas de aplicativo, etc., o aplicativo hello pode não suportar este cenário sem personalização. Neste caso é verdadeiro para algumas das estruturas populares de saudação que são abordadas Olá seções a seguir. Muitas perguntas vêm toomind quando você trabalha com estruturas/CMS, tais como:

- Como quebrar conteúdo Olá em ambientes diferentes?
- Quais arquivos você pode alterar sem afetar as atualizações de versão da estrutura?
- Como gerenciar as configurações por ambiente?
- Como gerenciar atualizações de versão de módulos, plug-ins e estrutura de principal Olá?

Há muitos tooset maneiras vários ambientes de seu projeto. Olá exemplos a seguir mostram um método para cada respectivo aplicativo.

### <a name="wordpress"></a>WordPress
Nesta seção, você aprenderá como tooset o fluxo de trabalho de um implantação usando slots de WordPress. O WordPress, como a maioria das soluções de CMS, não dá suporte a vários ambientes de desenvolvimento sem personalização. recurso de aplicativos Web de saudação do serviço de aplicativo do Azure tem alguns recursos que tornam mais fácil toostore definições de configuração fora de seu código.

1. Antes de criar um slot de preparo, configure seu toosupport de código do aplicativo vários ambientes. toosupport vários ambientes WordPress, é necessário tooedit `wp-config.php` em seu local de desenvolvimento aplicativo da web e adicionar Olá seguindo o código no início de saudação do arquivo hello. Esse processo permite que seu aplicativo toopick Olá configuração correta com base no ambiente selecionado hello.

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. Criar uma pasta na raiz do aplicativo web chamado `config`e adicione Olá `wp-config.azure.php` e `wp-config.local.php` arquivos, que representam o ambiente do Azure e o ambiente local, respectivamente.

3. Copie a seguinte Olá em `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Definir chaves de segurança Olá conforme ilustrado no código anterior Olá pode ajudar tooprevent seu aplicativo web de sendo invadido, portanto, use valores exclusivos. Se precisar de cadeia de caracteres de saudação toogenerate para chaves de segurança mencionadas no código hello, você pode [gerador automática vá toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate novos pares chave/valor.

4. Código a seguir de saudação de cópia em `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>Use caminhos relativos
Uma última tooconfigure de coisa no aplicativo de WordPress Olá é caminhos relativos. WordPress armazena informações de URL no banco de dados de saudação. Esse armazenamento dificultará a mover o conteúdo de um ambiente tooanother. É necessário o banco de dados do tooupdate Olá toda vez que você mover de toostage local ou ambientes de tooproduction estágio. risco de saudação tooreduce dos problemas que podem ocorrer com a implantação de um banco de dados sempre que você implantar a partir de um ambiente tooanother, use Olá [relativo raiz vincula o plug-in](https://wordpress.org/plugins/root-relative-urls/), que pode ser instalado usando o administrador do WordPress Olá Painel de controle.

Adicionar Olá tooyour entradas a seguir `wp-config.php` arquivo antes de saudação `That's all, stop editing!` comentário:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Ativar Olá plug-in por meio de saudação `Plugins` menu no painel do administrador de WordPress. Salve as configurações de link permanente para o aplicativo WordPress.

#### <a name="hello-final-wp-configphp-file"></a>Olá final `wp-config.php` arquivo
As atualizações principais do WordPress não afetarão seus arquivos `wp-config.php`, `wp-config.azure.php` e `wp-config.local.php`. Esta é a versão final do hello `wp-config.php` arquivo:

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Configurar um ambiente de preparo
1. Se você já tiver um aplicativo web do WordPress em execução em sua assinatura do Azure, entre no toohello [portal do Azure](http://portal.azure.com), e, em seguida, vá tooyour WordPress web app. Se você não tiver um aplicativo web do WordPress, você pode criar um de saudação do Azure Marketplace. mais, consulte toolearn [criar um aplicativo web do WordPress no serviço de aplicativo do Azure](web-sites-php-web-site-gallery.md).
Clique em **configurações** > **slots de implantação** > **adicionar** toocreate um slot de implantação com o nome da saudação *estágio*. Um slot de implantação é outro aplicativo web que compartilhamentos Olá os mesmos recursos que o aplicativo web principal de saudação que você criou anteriormente.

    ![Criar um slot de implantação de estágio](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Adicionar outro banco de dados MySQL, digamos que `wordpress-stage-db`, grupo de recursos de tooyour `wordpressapp-group`.

    ![Adicionar grupo de tooresource de banco de dados MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Atualizar cadeias de caracteres de conexão de saudação do estágio implantação slot toopoint toohello novo banco de dados, `wordpress-stage-db`. O aplicativo web de produção, `wordpressprodapp`e de preparo do aplicativo web, `wordpressprodapp-stage`, bancos de dados deve toodifferent ponto.

#### <a name="configure-environment-specific-app-settings"></a>Definir configurações específicas do ambiente de aplicativo
Os desenvolvedores podem armazenar pares de cadeia de caracteres de chave/valor no Azure como parte das informações de configuração hello, chamadas **configurações do aplicativo**, associado a um aplicativo web. Em tempo de execução, os aplicativos web automaticamente recuperam esses valores e torná-los disponível toocode que está sendo executado no seu aplicativo web. Do ponto de vista da segurança, é um bom benefício indireto, pois informações confidenciais, como cadeias de conexão de banco de dados que incluem senhas, nunca aparecem como texto não criptografado em um arquivo como o `wp-config.php`.

Esse processo, que é explicado em Olá parágrafos a seguir, é útil porque ela inclui alterações de arquivo e alterações de banco de dados para o aplicativo de WordPress Olá:

* Atualização de versão do WordPress
* Adicionar novo, editar ou atualizar plug-ins
* Adicionar novo, editar ou atualizar temas

Definir configurações do aplicativo para:

* Informações de banco de dados
* Habilitar/desabilitar o registro em log do WordPress
* Configurações de segurança do WordPress

![Configurações de Aplicativo para aplicativo Web Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Certifique-se de que você adicione Olá seguindo as configurações do aplicativo para o slot de produção web app e estágio. Observe que a saudação aplicativo da web de produção e preparo aplicativo da web usam bancos de dados diferentes.

1. Olá limpar **configuração do Slot** caixa de seleção para todos os parâmetros de configurações de saudação exceto WP_ENV. Esse processo alternará configuração Olá para seu aplicativo web, o conteúdo do arquivo e o banco de dados. Se **configuração do Slot** é verificado, configurações do aplicativo e a configuração de cadeia de caracteres de conexão do aplicativo da web de saudação serão *não* mover entre ambientes ao fazer uma **trocar** operação. As alterações de banco de dados presentes não interromperão o aplicativo Web de produção.

2. Implante Olá desenvolvimento local ambiente web aplicativo toohello estágio web app e o banco de dados usando o WebMatrix ou ferramentas de sua escolha, como FTP, Git ou PhpMyAdmin.

    ![Caixa de Diálogo Publicação do Web Matrix no aplicativo Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Procurar e testar seu aplicativo Web de preparo. Considerar um cenário em que o tema de saudação do aplicativo web de saudação é toobe atualizado, aqui é Olá aplicativo web de preparo.

    ![Procurar aplicativo Web de preparo antes de alternar slots](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Se tudo estiver correto, clique em Olá **trocar** botão seu ambiente de produção de conteúdo toohello o preparo toomove de aplicativo web. Nesse caso, você pode trocar Olá web app e o banco de dados de saudação em ambientes durante cada **permuta** operação.

    ![Alternar alterações de visualização do WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Se seu cenário precisa enviar tooonly os arquivos (atualizações de banco de dados), verifique **configuração do Slot** para todos os Olá relacionados ao banco de dados *configurações do aplicativo* e *configuraçõesdecadeiasdecaracteresdeconexão*em Olá **configurações do aplicativo Web** folha em Olá portal do Azure antes de fazer Olá **trocar**. Neste caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, as configurações de cadeia de conexão padrão devem aparecer nas alterações de visualização ao realizar a **Troca**. Neste momento, quando você concluir Olá **trocar** operação, Olá aplicativo web do WordPress será ter Olá atualiza somente os arquivos.
    >
    >

    Antes de fazer uma **trocar**, aqui está o aplicativo de web do WordPress de produção de hello.
    ![Aplicativo Web de produção antes de trocar slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Depois de saudação **trocar** operação, tema Olá foi atualizada em seu aplicativo da web de produção.

    ![Aplicativo Web de produção após alternar slots](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Quando você precisar tooroll novamente, você pode ir web de produção toohello **configurações do aplicativo**e clique em Olá **trocar** botão tooswap Olá web app e o banco de dados toostaging no slot de produção. Lembre-se de que se as alterações do banco de dados são incluídas com um **trocar** operação, em seguida, Olá próxima vez que você implantar tooyour preparo aplicativo web, é necessário toodeploy Olá alterações toohello atual banco de dados para seu aplicativo web preparo. banco de dados atual Olá pode ser banco de dados de produção de anterior hello ou Olá estágio.

#### <a name="summary"></a>Resumo
Veja a seguir um processo generalizado para qualquer aplicativo que tenha um banco de dados:

1. Instale o aplicativo hello em seu ambiente local.
2. Inclua configurações específicas de ambiente (locais e Aplicativos Web do Azure).
3. Configure seus ambientes de produção e preparo para aplicativos Web.
4. Se você tiver um aplicativo de produção já em execução no Azure, sincronize seu conteúdo (arquivos/código e banco de dados) toolocal e preparo ambientes de produção.
5. Desenvolva seu aplicativo no ambiente local.
6. Coloque seu aplicativo da web de produção em manutenção ou modo bloqueado e sincronizar o conteúdo do banco de dados toostaging e desenvolvimento de ambientes de produção.
7. Implante toohello teste e ambiente de preparo.
8. Implante ambiente tooproduction.
9. Repita as etapas quatro a seis.

### <a name="umbraco"></a>Umbraco
Nesta seção, você aprenderá como Olá Umbraco CMS usa um módulo personalizado toodeploy em vários ambientes de DevOps. Este exemplo fornece uma abordagem diferente toomanaging vários ambientes de desenvolvimento.

[Umbraco CMS](http://umbraco.com/) é uma solução de .NET CMS popular usada por muitos desenvolvedores. Ele fornece Olá [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy do módulo de ambientes de desenvolvimento de tooproduction toostaging. Você pode criar facilmente um ambiente de desenvolvimento local para um aplicativo Web Umbraco CMS usando o Visual Studio ou o WebMatrix.

- [Criar um aplicativo Web Umbraco com o Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Criar um aplicativo Web Umbraco com o WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Lembre-se sempre Olá tooremove `install` pasta em seu aplicativo e nunca carregá-lo a aplicativos web de toostage ou de produção. Este tutorial usa o WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Configurar um ambiente de preparo
1. Crie um slot de implantação, conforme mencionado anteriormente para Olá Umbraco CMS web app, supondo que você já tiver um aplicativo da web Umbraco CMS para cima e em execução. Se você não fizer isso, você pode criar um da saudação Marketplace.
2. Atualizar a cadeia de caracteres de conexão de saudação para seu novo de toohello estágio toopoint do slot de implantação **umbraco de estágio de db** banco de dados. O aplicativo web de produção (umbraositecms-1) e o preparo web app (etapas de 1 umbracositecms) *deve* toodifferent de ponto de bancos de dados.

    ![Atualizar a Cadeia de conexão para aplicativos Web de preparo com o novo banco de dados de preparo](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Clique em **configurações de publicação obter** para o slot de implantação Olá **estágio**. Esse processo baixará um arquivo de configurações de publicação que armazena todas as informações de saudação que o Visual Studio ou no WebMatrix requer toopublish seu aplicativo do aplicativo de web do Azure toohello do aplicativo de web de desenvolvimento local hello.

    ![Obter configuração de saudação preparo aplicativo web de publicação](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Abra seu aplicativo Web de desenvolvimento local no WebMatrix ou Visual Studio. Este tutorial usa o WebMatrix. Primeiro, é necessário tooimport Olá publicar o arquivo de configurações para seu aplicativo web preparo.

    ![Importar Configurações de publicação para o Umbraco usando Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Revisar as alterações na caixa de diálogo hello e implantar seu aplicativo de web do Azure de tooyour de aplicativo da web local, *umbracositecms-1-estágio*. Quando você implantar arquivos diretamente tooyour preparação de aplicativo da web, você será omitir os arquivos no hello `~/app_data/TEMP/` pasta porque esses arquivos serão regenerados quando é o primeiro aplicativo de web de estágio Olá iniciado. Você também deve omitir Olá `~/app_data/umbraco.config` arquivo, que também será regenerado.

    ![Examinar as alterações de publicação no Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Depois de publicar Olá Umbraco web local aplicativo toohello preparo aplicativo web com êxito, procurar tooyour preparo web app e execute toorule de testes alguns problemas.

#### <a name="set-up-hello-courier2-deployment-module"></a>Configurar o módulo de implantação Courier2 Olá
Com hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) módulo, simplesmente clique toopush conteúdo, folhas de estilo e módulos de desenvolvimento de um teste da web aplicativo tooa aplicativo web de produção. Esse processo reduz o risco de saudação de quebrar seu aplicativo da web de produção quando você implantar uma atualização.
Adquira uma licença para Courier2 para Olá `*.azurewebsites.net` domínio e seu domínio personalizado (digamos http://abc.com). Depois de comprar licenças hello, Olá local baixado licença (. Arquivo lic.) no hello `bin` pasta.

![Soltar o arquivo de licença na pasta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Baixe o pacote de saudação Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Logon no aplicativo web do estágio tooyour, digamos que http://umbracocms-site-stage.azurewebsites.net/umbraco, clique em Olá **desenvolvedor** menu e clique **pacotes** > **instalar pacote local**.

    ![Instalador do pacote Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Carregar o pacote de saudação Courier2 usando o instalador de saudação.

    ![Carregar pacote para módulo courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. pacote de saudação tooconfigure, você precisa courier.config arquivo hello tooupdate Olá **Config** pasta do seu aplicativo web.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. Em `<repositories>`, insira as informações de usuário e a URL de site de produção do hello.
    Se você estiver usando o provedor de associação saudação padrão Umbraco, adicionar Olá ID de usuário de administração de saudação em Olá &lt;usuário&gt; seção.
    Se você estiver usando um provedor de associação personalizado Umbraco, use `<login>`,`<password>` no site de produção do hello Courier2 módulo tooconnect toohello.
    Para obter mais detalhes, [documentação Olá módulo Olá Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Da mesma forma, instalar o módulo de Courier2 de saudação em seu site de produção e configurá-lo toopoint toohello estágio web app em seu arquivo do respectivos courier.config conforme mostrado aqui.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Clique em Olá **Courier2** guia Olá painel do aplicativo web Umbraco CMS e, em seguida, clique em **locais**. Você deve ver o nome do repositório Olá conforme mencionado em `courier.config`. Faça esse processo em seus aplicativos Web de preparo e de produção.

    ![Exibir repositório de aplicativo Web de destino](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. conteúdo toodeploy Olá preparo site de produção do site toohello, ir muito**conteúdo**e selecione uma página existente ou crie uma nova página. Seleciono uma página existente do meu aplicativo web em que o título de saudação da página de saudação é **Introdução – nova**e, em seguida, clique em **salvar e publicar**.

    ![Alterar o título da página e publicar](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Olá com o botão direito modificado página tooview todas as opções de saudação. Clique em **Courier** tooopen Olá **implantação** caixa de diálogo. Clique em **implantar** tooinitiate implantação.

    ![Diálogo de implantação de módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Revisar alterações hello e, em seguida, clique em **continuar**.

    ![Alterações de análise do diálogo de implantação de módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    log de implantação Olá mostra se a implantação de saudação foi bem-sucedida.

     ![Exibir Logs de implantação do módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Procure seu toosee de aplicativo de web de produção se Olá alterações são refletidas.

     ![Procurar o aplicativo Web de produção](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

toolearn mais sobre como toouse Courier, examine Olá documentação.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Como tooupgrade Olá versão Umbraco CMS
Será Courier não ajudam a atualizar de uma versão do tooanother Umbraco CMS. Quando você atualiza uma versão Umbraco CMS, deve verificar se há incompatibilidades com seus módulos personalizados ou de parceiros e Olá Umbraco Core libraries. Estas são as práticas recomendadas:

* Sempre faça backup de seu aplicativo Web e do banco de dados antes de fazer uma atualização. Em aplicativos web no Azure, você pode configurar backups automáticos para seus sites usando o recurso de backup hello e restaurar seu site, se necessário, usando o recurso de restauração de saudação. Para obter mais detalhes, consulte [como tooback o seu aplicativo web](web-sites-backup.md) e [como toorestore seu aplicativo web](web-sites-restore.md).
* Verifique se os pacotes de parceiros são compatíveis com versão Olá que estiver atualizando para o. Página de download do pacote hello, examine a compatibilidade de projeto Olá com uma versão Umbraco CMS.

Para obter mais detalhes sobre como tooupgrade seu aplicativo web localmente, [Consulte diretrizes gerais de atualização Olá](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Depois que o site de desenvolvimento local for atualizado, publica Olá alterações toohello aplicativo web de preparo. Teste seu aplicativo. Se tudo estiver correto, use Olá **trocar** botão tooswap seu aplicativo de web de produção do site toohello preparo. Quando você usa Olá **trocar** operação, você pode exibir as alterações de saudação que serão afetadas na configuração do seu aplicativo web. Isso **trocar** operação alterna Olá os aplicativos web e os bancos de dados. Depois de saudação **trocar**, Olá produção aplicativo será toohello ponto umbraco de estágio de db banco de dados web e Olá preparo web aplicativo será ponto tooumbraco-prod-db banco de dados.

![Alternar visualização para implantar o Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Estas são as vantagens de troca Olá web app e o banco de dados de saudação:

* Você pode reverter toohello a versão anterior de seu aplicativo web com outra **trocar** se houver algum problema de aplicativo.
* Para uma atualização, você precisa toodeploy arquivos e bancos de dados de saudação preparo aplicativo de web de produção do toohello de aplicativo web e banco de dados. Muitas coisas que podem dar errado quando você implanta arquivos e bancos de dados. Usando Olá **trocar** recurso de slots, podemos reduzir o tempo de inatividade durante uma atualização e reduzir o risco de saudação de falhas que podem ocorrer quando você implantar as alterações.
* Você pode fazer **A / B teste** usando Olá [teste em produção](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) recurso.

Este exemplo mostra Olá flexibilidade da plataforma Olá onde você pode criar módulos personalizados semelhante tooUmbraco Courier toomanage a implantação do módulo em ambientes.

## <a name="references"></a>Referências
[Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure](app-service-agile-software-development.md)

[Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-staged-publishing.md)

[Como o web tooblock acessar slots de implantação de produção toonon](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
