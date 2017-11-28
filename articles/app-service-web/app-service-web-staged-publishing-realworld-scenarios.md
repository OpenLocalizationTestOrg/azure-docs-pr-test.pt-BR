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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="fb1f7-103">Usar ambientes de Operações de Desenvolvimento com eficiência em seus aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="fb1f7-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="fb1f7-104">Este artigo mostra como tooset e gerenciar implantações de aplicativo web quando várias versões do seu aplicativo em vários ambientes, como desenvolvimento, teste, qualidade (QA) e produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="fb1f7-105">Cada versão do seu aplicativo pode ser considerado como um ambiente de desenvolvimento para finalidade específica de saudação do processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="fb1f7-106">Por exemplo, os desenvolvedores podem usar Olá qualidade do controle de qualidade ambiente tootest saudação do aplicativo hello antes de eles push Olá alterações tooproduction.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="fb1f7-107">Vários ambientes de desenvolvimento podem ser um desafio porque você precisa de código tootrack, gerenciar recursos (computação, aplicativo web, banco de dados, cache, etc.) e implante o código em ambientes.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="fb1f7-108">Configurar um ambiente de não produção (estágio, desenvolvimento, controle de qualidade)</span><span class="sxs-lookup"><span data-stu-id="fb1f7-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="fb1f7-109">Depois que um aplicativo da web de produção estiver em execução, Olá próxima etapa é toocreate um ambiente de não produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="fb1f7-110">toouse slots de implantação, certifique-se de que você está executando no modo de plano Standard ou o serviço de aplicativo do Azure Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="fb1f7-111">Os slots de implantação são aplicativos Web dinâmicos com seus próprios nomes de host.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="fb1f7-112">Elementos de conteúdo e configuração de aplicativo da Web podem ser trocados entre os dois slots de implantação, incluindo o slot de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="fb1f7-113">Quando você implanta o slot de implantação do aplicativo tooa, você obtém Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="fb1f7-114">Você pode validar o aplicativo de web tooa alterações em um slot de implantação de preparo antes de alternar o aplicativo hello com o slot de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="fb1f7-115">Quando você implanta um slot de tooa do aplicativo web primeiro e troque-o em produção, todas as instâncias do slot de saudação são aquecidas antes de ser trocadas em produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="fb1f7-116">Esse processo elimina o tempo de inatividade quando você for implantar seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="fb1f7-117">Olá redirecionamento do tráfego é contínuo e nenhuma solicitação é descartada devido a operações de tooswap.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="fb1f7-118">tooautomate esse fluxo de trabalho inteiro, configurar [troca automática](web-sites-staged-publishing.md#configure-auto-swap) quando a validação de pré-permuta não é necessária.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="fb1f7-119">Após uma troca slot Olá que tem o aplicativo web de saudação preparado anteriormente agora tem Olá aplicativo de web de produção anterior.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="fb1f7-120">Se alterações Olá trocadas no slot de produção de hello estiverem não conforme o esperado, você pode executar Olá mesma troca imediatamente tooget seu "última boas" back do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="fb1f7-121">tooset backup de um slot de implantação de preparo, consulte [configurar ambientes de preparo para aplicativos web no serviço de aplicativo do Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="fb1f7-122">Cada ambiente deve incluir seu próprio conjunto de recursos.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="fb1f7-123">Por exemplo, se o seu aplicativo Web usar um banco de dados, os aplicativos Web de preparo e produção deverão usar bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="fb1f7-124">Adicione seu ambiente de desenvolvimento de preparo de preparo recursos do ambiente de desenvolvimento como tooset de cache, armazenamento ou banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="fb1f7-125">Exemplos de uso de vários ambientes de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="fb1f7-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="fb1f7-126">Qualquer projeto deve seguir o gerenciamento de código fonte com pelo menos dois ambientes: desenvolvimento e produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="fb1f7-127">Se você usar sistemas de gerenciamento de conteúdo (CMSs), estruturas de aplicativo, etc., o aplicativo hello pode não suportar este cenário sem personalização.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="fb1f7-128">Neste caso é verdadeiro para algumas das estruturas populares de saudação que são abordadas Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="fb1f7-129">Muitas perguntas vêm toomind quando você trabalha com estruturas/CMS, tais como:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="fb1f7-130">Como quebrar conteúdo Olá em ambientes diferentes?</span><span class="sxs-lookup"><span data-stu-id="fb1f7-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="fb1f7-131">Quais arquivos você pode alterar sem afetar as atualizações de versão da estrutura?</span><span class="sxs-lookup"><span data-stu-id="fb1f7-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="fb1f7-132">Como gerenciar as configurações por ambiente?</span><span class="sxs-lookup"><span data-stu-id="fb1f7-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="fb1f7-133">Como gerenciar atualizações de versão de módulos, plug-ins e estrutura de principal Olá?</span><span class="sxs-lookup"><span data-stu-id="fb1f7-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="fb1f7-134">Há muitos tooset maneiras vários ambientes de seu projeto.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="fb1f7-135">Olá exemplos a seguir mostram um método para cada respectivo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="fb1f7-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="fb1f7-136">WordPress</span></span>
<span data-ttu-id="fb1f7-137">Nesta seção, você aprenderá como tooset o fluxo de trabalho de um implantação usando slots de WordPress.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="fb1f7-138">O WordPress, como a maioria das soluções de CMS, não dá suporte a vários ambientes de desenvolvimento sem personalização.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="fb1f7-139">recurso de aplicativos Web de saudação do serviço de aplicativo do Azure tem alguns recursos que tornam mais fácil toostore definições de configuração fora de seu código.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="fb1f7-140">Antes de criar um slot de preparo, configure seu toosupport de código do aplicativo vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="fb1f7-141">toosupport vários ambientes WordPress, é necessário tooedit `wp-config.php` em seu local de desenvolvimento aplicativo da web e adicionar Olá seguindo o código no início de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="fb1f7-142">Esse processo permite que seu aplicativo toopick Olá configuração correta com base no ambiente selecionado hello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="fb1f7-143">Criar uma pasta na raiz do aplicativo web chamado `config`e adicione Olá `wp-config.azure.php` e `wp-config.local.php` arquivos, que representam o ambiente do Azure e o ambiente local, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="fb1f7-144">Copie a seguinte Olá em `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="fb1f7-145">Definir chaves de segurança Olá conforme ilustrado no código anterior Olá pode ajudar tooprevent seu aplicativo web de sendo invadido, portanto, use valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="fb1f7-146">Se precisar de cadeia de caracteres de saudação toogenerate para chaves de segurança mencionadas no código hello, você pode [gerador automática vá toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate novos pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="fb1f7-147">Código a seguir de saudação de cópia em `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="fb1f7-148">Use caminhos relativos</span><span class="sxs-lookup"><span data-stu-id="fb1f7-148">Use relative paths</span></span>
<span data-ttu-id="fb1f7-149">Uma última tooconfigure de coisa no aplicativo de WordPress Olá é caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="fb1f7-150">WordPress armazena informações de URL no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="fb1f7-151">Esse armazenamento dificultará a mover o conteúdo de um ambiente tooanother.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="fb1f7-152">É necessário o banco de dados do tooupdate Olá toda vez que você mover de toostage local ou ambientes de tooproduction estágio.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="fb1f7-153">risco de saudação tooreduce dos problemas que podem ocorrer com a implantação de um banco de dados sempre que você implantar a partir de um ambiente tooanother, use Olá [relativo raiz vincula o plug-in](https://wordpress.org/plugins/root-relative-urls/), que pode ser instalado usando o administrador do WordPress Olá Painel de controle.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="fb1f7-154">Adicionar Olá tooyour entradas a seguir `wp-config.php` arquivo antes de saudação `That's all, stop editing!` comentário:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="fb1f7-155">Ativar Olá plug-in por meio de saudação `Plugins` menu no painel do administrador de WordPress.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="fb1f7-156">Salve as configurações de link permanente para o aplicativo WordPress.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="fb1f7-157">Olá final `wp-config.php` arquivo</span><span class="sxs-lookup"><span data-stu-id="fb1f7-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="fb1f7-158">As atualizações principais do WordPress não afetarão seus arquivos `wp-config.php`, `wp-config.azure.php` e `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="fb1f7-159">Esta é a versão final do hello `wp-config.php` arquivo:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="fb1f7-160">Configurar um ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="fb1f7-160">Set up a staging environment</span></span>
1. <span data-ttu-id="fb1f7-161">Se você já tiver um aplicativo web do WordPress em execução em sua assinatura do Azure, entre no toohello [portal do Azure](http://portal.azure.com), e, em seguida, vá tooyour WordPress web app.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="fb1f7-162">Se você não tiver um aplicativo web do WordPress, você pode criar um de saudação do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="fb1f7-163">mais, consulte toolearn [criar um aplicativo web do WordPress no serviço de aplicativo do Azure](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="fb1f7-164">Clique em **configurações** > **slots de implantação** > **adicionar** toocreate um slot de implantação com o nome da saudação *estágio*.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="fb1f7-165">Um slot de implantação é outro aplicativo web que compartilhamentos Olá os mesmos recursos que o aplicativo web principal de saudação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Criar um slot de implantação de estágio](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="fb1f7-167">Adicionar outro banco de dados MySQL, digamos que `wordpress-stage-db`, grupo de recursos de tooyour `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![Adicionar grupo de tooresource de banco de dados MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="fb1f7-169">Atualizar cadeias de caracteres de conexão de saudação do estágio implantação slot toopoint toohello novo banco de dados, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="fb1f7-170">O aplicativo web de produção, `wordpressprodapp`e de preparo do aplicativo web, `wordpressprodapp-stage`, bancos de dados deve toodifferent ponto.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="fb1f7-171">Definir configurações específicas do ambiente de aplicativo</span><span class="sxs-lookup"><span data-stu-id="fb1f7-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="fb1f7-172">Os desenvolvedores podem armazenar pares de cadeia de caracteres de chave/valor no Azure como parte das informações de configuração hello, chamadas **configurações do aplicativo**, associado a um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="fb1f7-173">Em tempo de execução, os aplicativos web automaticamente recuperam esses valores e torná-los disponível toocode que está sendo executado no seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="fb1f7-174">Do ponto de vista da segurança, é um bom benefício indireto, pois informações confidenciais, como cadeias de conexão de banco de dados que incluem senhas, nunca aparecem como texto não criptografado em um arquivo como o `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="fb1f7-175">Esse processo, que é explicado em Olá parágrafos a seguir, é útil porque ela inclui alterações de arquivo e alterações de banco de dados para o aplicativo de WordPress Olá:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="fb1f7-176">Atualização de versão do WordPress</span><span class="sxs-lookup"><span data-stu-id="fb1f7-176">WordPress version upgrade</span></span>
* <span data-ttu-id="fb1f7-177">Adicionar novo, editar ou atualizar plug-ins</span><span class="sxs-lookup"><span data-stu-id="fb1f7-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="fb1f7-178">Adicionar novo, editar ou atualizar temas</span><span class="sxs-lookup"><span data-stu-id="fb1f7-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="fb1f7-179">Definir configurações do aplicativo para:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-179">Configure app settings for:</span></span>

* <span data-ttu-id="fb1f7-180">Informações de banco de dados</span><span class="sxs-lookup"><span data-stu-id="fb1f7-180">Database information</span></span>
* <span data-ttu-id="fb1f7-181">Habilitar/desabilitar o registro em log do WordPress</span><span class="sxs-lookup"><span data-stu-id="fb1f7-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="fb1f7-182">Configurações de segurança do WordPress</span><span class="sxs-lookup"><span data-stu-id="fb1f7-182">WordPress security settings</span></span>

![Configurações de Aplicativo para aplicativo Web Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="fb1f7-184">Certifique-se de que você adicione Olá seguindo as configurações do aplicativo para o slot de produção web app e estágio.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="fb1f7-185">Observe que a saudação aplicativo da web de produção e preparo aplicativo da web usam bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="fb1f7-186">Olá limpar **configuração do Slot** caixa de seleção para todos os parâmetros de configurações de saudação exceto WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="fb1f7-187">Esse processo alternará configuração Olá para seu aplicativo web, o conteúdo do arquivo e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="fb1f7-188">Se **configuração do Slot** é verificado, configurações do aplicativo e a configuração de cadeia de caracteres de conexão do aplicativo da web de saudação serão *não* mover entre ambientes ao fazer uma **trocar** operação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="fb1f7-189">As alterações de banco de dados presentes não interromperão o aplicativo Web de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="fb1f7-190">Implante Olá desenvolvimento local ambiente web aplicativo toohello estágio web app e o banco de dados usando o WebMatrix ou ferramentas de sua escolha, como FTP, Git ou PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Caixa de Diálogo Publicação do Web Matrix no aplicativo Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="fb1f7-192">Procurar e testar seu aplicativo Web de preparo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-192">Browse and test your staging web app.</span></span> <span data-ttu-id="fb1f7-193">Considerar um cenário em que o tema de saudação do aplicativo web de saudação é toobe atualizado, aqui é Olá aplicativo web de preparo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Procurar aplicativo Web de preparo antes de alternar slots](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="fb1f7-195">Se tudo estiver correto, clique em Olá **trocar** botão seu ambiente de produção de conteúdo toohello o preparo toomove de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="fb1f7-196">Nesse caso, você pode trocar Olá web app e o banco de dados de saudação em ambientes durante cada **permuta** operação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Alternar alterações de visualização do WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="fb1f7-198">Se seu cenário precisa enviar tooonly os arquivos (atualizações de banco de dados), verifique **configuração do Slot** para todos os Olá relacionados ao banco de dados *configurações do aplicativo* e *configuraçõesdecadeiasdecaracteresdeconexão*em Olá **configurações do aplicativo Web** folha em Olá portal do Azure antes de fazer Olá **trocar**.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="fb1f7-199">Neste caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, as configurações de cadeia de conexão padrão devem aparecer nas alterações de visualização ao realizar a **Troca**.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="fb1f7-200">Neste momento, quando você concluir Olá **trocar** operação, Olá aplicativo web do WordPress será ter Olá atualiza somente os arquivos.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="fb1f7-201">Antes de fazer uma **trocar**, aqui está o aplicativo de web do WordPress de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="fb1f7-202">![Aplicativo Web de produção antes de trocar slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="fb1f7-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="fb1f7-203">Depois de saudação **trocar** operação, tema Olá foi atualizada em seu aplicativo da web de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Aplicativo Web de produção após alternar slots](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="fb1f7-205">Quando você precisar tooroll novamente, você pode ir web de produção toohello **configurações do aplicativo**e clique em Olá **trocar** botão tooswap Olá web app e o banco de dados toostaging no slot de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="fb1f7-206">Lembre-se de que se as alterações do banco de dados são incluídas com um **trocar** operação, em seguida, Olá próxima vez que você implantar tooyour preparo aplicativo web, é necessário toodeploy Olá alterações toohello atual banco de dados para seu aplicativo web preparo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="fb1f7-207">banco de dados atual Olá pode ser banco de dados de produção de anterior hello ou Olá estágio.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="fb1f7-208">Resumo</span><span class="sxs-lookup"><span data-stu-id="fb1f7-208">Summary</span></span>
<span data-ttu-id="fb1f7-209">Veja a seguir um processo generalizado para qualquer aplicativo que tenha um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="fb1f7-210">Instale o aplicativo hello em seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="fb1f7-211">Inclua configurações específicas de ambiente (locais e Aplicativos Web do Azure).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="fb1f7-212">Configure seus ambientes de produção e preparo para aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="fb1f7-213">Se você tiver um aplicativo de produção já em execução no Azure, sincronize seu conteúdo (arquivos/código e banco de dados) toolocal e preparo ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="fb1f7-214">Desenvolva seu aplicativo no ambiente local.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="fb1f7-215">Coloque seu aplicativo da web de produção em manutenção ou modo bloqueado e sincronizar o conteúdo do banco de dados toostaging e desenvolvimento de ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="fb1f7-216">Implante toohello teste e ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="fb1f7-217">Implante ambiente tooproduction.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="fb1f7-218">Repita as etapas quatro a seis.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="fb1f7-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="fb1f7-219">Umbraco</span></span>
<span data-ttu-id="fb1f7-220">Nesta seção, você aprenderá como Olá Umbraco CMS usa um módulo personalizado toodeploy em vários ambientes de DevOps.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="fb1f7-221">Este exemplo fornece uma abordagem diferente toomanaging vários ambientes de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="fb1f7-222">[Umbraco CMS](http://umbraco.com/) é uma solução de .NET CMS popular usada por muitos desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="fb1f7-223">Ele fornece Olá [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy do módulo de ambientes de desenvolvimento de tooproduction toostaging.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="fb1f7-224">Você pode criar facilmente um ambiente de desenvolvimento local para um aplicativo Web Umbraco CMS usando o Visual Studio ou o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="fb1f7-225">Criar um aplicativo Web Umbraco com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb1f7-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="fb1f7-226">Criar um aplicativo Web Umbraco com o WebMatrix</span><span class="sxs-lookup"><span data-stu-id="fb1f7-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="fb1f7-227">Lembre-se sempre Olá tooremove `install` pasta em seu aplicativo e nunca carregá-lo a aplicativos web de toostage ou de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="fb1f7-228">Este tutorial usa o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="fb1f7-229">Configurar um ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="fb1f7-229">Set up a staging environment</span></span>
1. <span data-ttu-id="fb1f7-230">Crie um slot de implantação, conforme mencionado anteriormente para Olá Umbraco CMS web app, supondo que você já tiver um aplicativo da web Umbraco CMS para cima e em execução.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="fb1f7-231">Se você não fizer isso, você pode criar um da saudação Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="fb1f7-232">Atualizar a cadeia de caracteres de conexão de saudação para seu novo de toohello estágio toopoint do slot de implantação **umbraco de estágio de db** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="fb1f7-233">O aplicativo web de produção (umbraositecms-1) e o preparo web app (etapas de 1 umbracositecms) *deve* toodifferent de ponto de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Atualizar a Cadeia de conexão para aplicativos Web de preparo com o novo banco de dados de preparo](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="fb1f7-235">Clique em **configurações de publicação obter** para o slot de implantação Olá **estágio**.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="fb1f7-236">Esse processo baixará um arquivo de configurações de publicação que armazena todas as informações de saudação que o Visual Studio ou no WebMatrix requer toopublish seu aplicativo do aplicativo de web do Azure toohello do aplicativo de web de desenvolvimento local hello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Obter configuração de saudação preparo aplicativo web de publicação](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="fb1f7-238">Abra seu aplicativo Web de desenvolvimento local no WebMatrix ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="fb1f7-239">Este tutorial usa o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="fb1f7-240">Primeiro, é necessário tooimport Olá publicar o arquivo de configurações para seu aplicativo web preparo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Importar Configurações de publicação para o Umbraco usando Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="fb1f7-242">Revisar as alterações na caixa de diálogo hello e implantar seu aplicativo de web do Azure de tooyour de aplicativo da web local, *umbracositecms-1-estágio*.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="fb1f7-243">Quando você implantar arquivos diretamente tooyour preparação de aplicativo da web, você será omitir os arquivos no hello `~/app_data/TEMP/` pasta porque esses arquivos serão regenerados quando é o primeiro aplicativo de web de estágio Olá iniciado.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="fb1f7-244">Você também deve omitir Olá `~/app_data/umbraco.config` arquivo, que também será regenerado.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Examinar as alterações de publicação no Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="fb1f7-246">Depois de publicar Olá Umbraco web local aplicativo toohello preparo aplicativo web com êxito, procurar tooyour preparo web app e execute toorule de testes alguns problemas.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="fb1f7-247">Configurar o módulo de implantação Courier2 Olá</span><span class="sxs-lookup"><span data-stu-id="fb1f7-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="fb1f7-248">Com hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) módulo, simplesmente clique toopush conteúdo, folhas de estilo e módulos de desenvolvimento de um teste da web aplicativo tooa aplicativo web de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="fb1f7-249">Esse processo reduz o risco de saudação de quebrar seu aplicativo da web de produção quando você implantar uma atualização.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="fb1f7-250">Adquira uma licença para Courier2 para Olá `*.azurewebsites.net` domínio e seu domínio personalizado (digamos http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="fb1f7-251">Depois de comprar licenças hello, Olá local baixado licença (. Arquivo lic.) no hello `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Soltar o arquivo de licença na pasta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="fb1f7-253">[Baixe o pacote de saudação Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="fb1f7-254">Logon no aplicativo web do estágio tooyour, digamos que http://umbracocms-site-stage.azurewebsites.net/umbraco, clique em Olá **desenvolvedor** menu e clique **pacotes** > **instalar pacote local**.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Instalador do pacote Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="fb1f7-256">Carregar o pacote de saudação Courier2 usando o instalador de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Carregar pacote para módulo courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="fb1f7-258">pacote de saudação tooconfigure, você precisa courier.config arquivo hello tooupdate Olá **Config** pasta do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="fb1f7-259">Em `<repositories>`, insira as informações de usuário e a URL de site de produção do hello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="fb1f7-260">Se você estiver usando o provedor de associação saudação padrão Umbraco, adicionar Olá ID de usuário de administração de saudação em Olá &lt;usuário&gt; seção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="fb1f7-261">Se você estiver usando um provedor de associação personalizado Umbraco, use `<login>`,`<password>` no site de produção do hello Courier2 módulo tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="fb1f7-262">Para obter mais detalhes, [documentação Olá módulo Olá Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="fb1f7-263">Da mesma forma, instalar o módulo de Courier2 de saudação em seu site de produção e configurá-lo toopoint toohello estágio web app em seu arquivo do respectivos courier.config conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="fb1f7-264">Clique em Olá **Courier2** guia Olá painel do aplicativo web Umbraco CMS e, em seguida, clique em **locais**.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="fb1f7-265">Você deve ver o nome do repositório Olá conforme mencionado em `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="fb1f7-266">Faça esse processo em seus aplicativos Web de preparo e de produção.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-266">Do this process on both your production and staging web apps.</span></span>

    ![Exibir repositório de aplicativo Web de destino](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="fb1f7-268">conteúdo toodeploy Olá preparo site de produção do site toohello, ir muito**conteúdo**e selecione uma página existente ou crie uma nova página.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="fb1f7-269">Seleciono uma página existente do meu aplicativo web em que o título de saudação da página de saudação é **Introdução – nova**e, em seguida, clique em **salvar e publicar**.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Alterar o título da página e publicar](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="fb1f7-271">Olá com o botão direito modificado página tooview todas as opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="fb1f7-272">Clique em **Courier** tooopen Olá **implantação** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="fb1f7-273">Clique em **implantar** tooinitiate implantação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Diálogo de implantação de módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="fb1f7-275">Revisar alterações hello e, em seguida, clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-275">Review hello changes, and then click **Continue**.</span></span>

    ![Alterações de análise do diálogo de implantação de módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="fb1f7-277">log de implantação Olá mostra se a implantação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Exibir Logs de implantação do módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="fb1f7-279">Procure seu toosee de aplicativo de web de produção se Olá alterações são refletidas.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Procurar o aplicativo Web de produção](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="fb1f7-281">toolearn mais sobre como toouse Courier, examine Olá documentação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="fb1f7-282">Como tooupgrade Olá versão Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="fb1f7-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="fb1f7-283">Será Courier não ajudam a atualizar de uma versão do tooanother Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="fb1f7-284">Quando você atualiza uma versão Umbraco CMS, deve verificar se há incompatibilidades com seus módulos personalizados ou de parceiros e Olá Umbraco Core libraries.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="fb1f7-285">Estas são as práticas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-285">Here are best practices:</span></span>

* <span data-ttu-id="fb1f7-286">Sempre faça backup de seu aplicativo Web e do banco de dados antes de fazer uma atualização.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="fb1f7-287">Em aplicativos web no Azure, você pode configurar backups automáticos para seus sites usando o recurso de backup hello e restaurar seu site, se necessário, usando o recurso de restauração de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="fb1f7-288">Para obter mais detalhes, consulte [como tooback o seu aplicativo web](web-sites-backup.md) e [como toorestore seu aplicativo web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="fb1f7-289">Verifique se os pacotes de parceiros são compatíveis com versão Olá que estiver atualizando para o.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="fb1f7-290">Página de download do pacote hello, examine a compatibilidade de projeto Olá com uma versão Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="fb1f7-291">Para obter mais detalhes sobre como tooupgrade seu aplicativo web localmente, [Consulte diretrizes gerais de atualização Olá](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="fb1f7-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="fb1f7-292">Depois que o site de desenvolvimento local for atualizado, publica Olá alterações toohello aplicativo web de preparo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="fb1f7-293">Teste seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-293">Test your application.</span></span> <span data-ttu-id="fb1f7-294">Se tudo estiver correto, use Olá **trocar** botão tooswap seu aplicativo de web de produção do site toohello preparo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="fb1f7-295">Quando você usa Olá **trocar** operação, você pode exibir as alterações de saudação que serão afetadas na configuração do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="fb1f7-296">Isso **trocar** operação alterna Olá os aplicativos web e os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="fb1f7-297">Depois de saudação **trocar**, Olá produção aplicativo será toohello ponto umbraco de estágio de db banco de dados web e Olá preparo web aplicativo será ponto tooumbraco-prod-db banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Alternar visualização para implantar o Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="fb1f7-299">Estas são as vantagens de troca Olá web app e o banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="fb1f7-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="fb1f7-300">Você pode reverter toohello a versão anterior de seu aplicativo web com outra **trocar** se houver algum problema de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="fb1f7-301">Para uma atualização, você precisa toodeploy arquivos e bancos de dados de saudação preparo aplicativo de web de produção do toohello de aplicativo web e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="fb1f7-302">Muitas coisas que podem dar errado quando você implanta arquivos e bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="fb1f7-303">Usando Olá **trocar** recurso de slots, podemos reduzir o tempo de inatividade durante uma atualização e reduzir o risco de saudação de falhas que podem ocorrer quando você implantar as alterações.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="fb1f7-304">Você pode fazer **A / B teste** usando Olá [teste em produção](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) recurso.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="fb1f7-305">Este exemplo mostra Olá flexibilidade da plataforma Olá onde você pode criar módulos personalizados semelhante tooUmbraco Courier toomanage a implantação do módulo em ambientes.</span><span class="sxs-lookup"><span data-stu-id="fb1f7-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="fb1f7-306">Referências</span><span class="sxs-lookup"><span data-stu-id="fb1f7-306">References</span></span>
[<span data-ttu-id="fb1f7-307">Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="fb1f7-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="fb1f7-308">Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="fb1f7-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="fb1f7-309">Como o web tooblock acessar slots de implantação de produção toonon</span><span class="sxs-lookup"><span data-stu-id="fb1f7-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
