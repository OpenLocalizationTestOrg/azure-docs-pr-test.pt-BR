---
title: "Usar ambientes de DevOps com eficiência para seu aplicativo Web | Microsoft Docs"
description: "Saiba como usar os slots de implantação para configurar e gerenciar vários ambientes de desenvolvimento do aplicativo"
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
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="1bcf4-103">Usar ambientes de Operações de Desenvolvimento com eficiência em seus aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="1bcf4-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="1bcf4-104">Este artigo mostra como configurar e gerenciar implantações de aplicativo Web quando houver várias versões de seu aplicativo em vários ambientes, como desenvolvimento, preparo, QA (controle de qualidade) e produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="1bcf4-105">Cada versão do aplicativo pode ser considerada um ambiente de desenvolvimento para a finalidade específica de seu processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="1bcf4-106">Por exemplo os desenvolvedores podem usar o ambiente de QA para testar a qualidade do aplicativo antes de aplicar as alterações em produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="1bcf4-107">Ter vários ambientes de desenvolvimento pode ser algo desafiador, pois você precisa controlar o código, gerenciar os recursos (computação, aplicativo Web, banco de dados, cache, etc.) e implantar o código nos ambientes.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="1bcf4-108">Configurar um ambiente de não produção (estágio, desenvolvimento, controle de qualidade)</span><span class="sxs-lookup"><span data-stu-id="1bcf4-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="1bcf4-109">Quando um aplicativo Web de produção estiver em funcionamento, a próxima etapa será criar um ambiente de não produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="1bcf4-110">Para usar slots de implantação, verifique se você está executando no modo do plano do Serviço de Aplicativo do Azure Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="1bcf4-111">Os slots de implantação são aplicativos Web dinâmicos com seus próprios nomes de host.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="1bcf4-112">Os elementos de configuração e conteúdo de aplicativo Web podem ser permutados entre dois slots de implantação, incluindo o slot de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="1bcf4-113">Quando você implanta seu aplicativo em um slot de implantação, obtém os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="1bcf4-114">É possível validar as alterações no aplicativo Web em um slot de implantação de preparo antes de trocá-lo pelo slot de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="1bcf4-115">Quando você implanta primeiro um aplicativo Web em um slot e depois trocá-o para produção, todas as instâncias do slot são preparadas antes dessa troca.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="1bcf4-116">Esse processo elimina o tempo de inatividade quando você for implantar seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="1bcf4-117">O redirecionamento do tráfego é contínuo e nenhuma solicitação é descartada devido a operações de permuta.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="1bcf4-118">Para automatizar todo esse fluxo de trabalho, configure a [Troca Automática](web-sites-staged-publishing.md#configure-auto-swap) quando a validação pré-troca não for necessária.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="1bcf4-119">Após uma troca, o slot com o aplicativo Web preparado anteriormente terá o aplicativo Web de produção anterior.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="1bcf4-120">Se as modificações alternadas no slot de produção não forem o que você esperava, é possível fazer a mesma alternação imediatamente para ter o “último aplicativo Web bom” de volta.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="1bcf4-121">Para configurar um slot de implantação de preparo, confira [Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="1bcf4-122">Cada ambiente deve incluir seu próprio conjunto de recursos.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="1bcf4-123">Por exemplo, se o seu aplicativo Web usar um banco de dados, os aplicativos Web de preparo e produção deverão usar bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="1bcf4-124">Adicione recursos de ambiente de desenvolvimento de preparo, como banco de dados, armazenamento ou cache, para definir o ambiente de desenvolvimento de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="1bcf4-125">Exemplos de uso de vários ambientes de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="1bcf4-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="1bcf4-126">Qualquer projeto deve seguir o gerenciamento de código fonte com pelo menos dois ambientes: desenvolvimento e produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="1bcf4-127">Se você usar CMSs (sistemas de gerenciamento de conteúdo), estruturas de aplicativo etc., talvez o aplicativo não ofereça suporte a esse cenário sem personalização.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="1bcf4-128">Essa eventualidade é real para algumas das estruturas populares discutidas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="1bcf4-129">Muitas perguntas vêm à tona ao trabalhar com CMS/estruturas, como:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="1bcf4-130">Como dividir o conteúdo em ambientes diferentes?</span><span class="sxs-lookup"><span data-stu-id="1bcf4-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="1bcf4-131">Quais arquivos você pode alterar sem afetar as atualizações de versão da estrutura?</span><span class="sxs-lookup"><span data-stu-id="1bcf4-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="1bcf4-132">Como gerenciar as configurações por ambiente?</span><span class="sxs-lookup"><span data-stu-id="1bcf4-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="1bcf4-133">Como você gerencia atualizações de versão para módulos, plug-ins e estrutura principal?</span><span class="sxs-lookup"><span data-stu-id="1bcf4-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="1bcf4-134">Há várias maneiras de configurar vários ambientes para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="1bcf4-135">Os exemplos a seguir mostram um método para cada aplicativo respectivo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="1bcf4-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="1bcf4-136">WordPress</span></span>
<span data-ttu-id="1bcf4-137">Nesta seção, você aprenderá como configurar um fluxo de trabalho de implantação usando slots para WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="1bcf4-138">O WordPress, como a maioria das soluções de CMS, não dá suporte a vários ambientes de desenvolvimento sem personalização.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="1bcf4-139">O recurso Aplicativos Web do Serviço de Aplicativo do Azure tem alguns recursos que facilitam o armazenamento de definições de configuração fora de seu código.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="1bcf4-140">Antes de criar um slot de preparo, configure o código do aplicativo para dar suporte a vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="1bcf4-141">Para dar suporte a vários ambientes no WordPress, você precisa editar `wp-config.php` em seu aplicativo Web de desenvolvimento local e adicionar o código a seguir no início do arquivo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="1bcf4-142">Esse processo permitirá que seu aplicativo obtenha a configuração correta com base no ambiente selecionado.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

    ```
    // Support multiple environments
    // set the config file based on current environment
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
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="1bcf4-143">Crie uma pasta na raiz do aplicativo Web chamada `config` e adicione os arquivos `wp-config.azure.php` e `wp-config.local.php`, que representam o ambiente do Azure e o ambiente local respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="1bcf4-144">Copie o seguinte em `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-144">Copy the following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
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

    <span data-ttu-id="1bcf4-145">A definição das chaves de segurança, conforme ilustrado acima, pode ajudar a impedir que seu aplicativo Web seja invadido; portanto, use valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="1bcf4-146">Se você precisar gerar a cadeia de caracteres para as chaves de segurança mencionadas no código, [acesse o gerador automático](https://api.wordpress.org/secret-key/1.1/salt) para criar novos pares de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="1bcf4-147">Copie o seguinte código em `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-147">Copy the following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

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
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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

#### <a name="use-relative-paths"></a><span data-ttu-id="1bcf4-148">Use caminhos relativos</span><span class="sxs-lookup"><span data-stu-id="1bcf4-148">Use relative paths</span></span>
<span data-ttu-id="1bcf4-149">Por fim, configure caminhos relativos no aplicativo WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="1bcf4-150">O WordPress armazena informações de URL no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="1bcf4-151">Esse armazenamento dificulta mais a movimentação de conteúdo de um ambiente para outro.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="1bcf4-152">Você precisa atualizar o banco de dados sempre que mudar do ambiente local para o de preparo ou do ambiente de preparo para de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="1bcf4-153">Para reduzir o risco de problemas que podem ocorrer com a implantação de banco de dados sempre que você implantar de um ambiente para outro, use o [plug-in de links Relative Root](https://wordpress.org/plugins/root-relative-urls/) que pode ser instalado usando o painel de administrador do WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="1bcf4-154">Adicione as seguintes entradas ao arquivo `wp-config.php` antes do comentário `That's all, stop editing!`:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="1bcf4-155">Ative o plug-in no menu `Plugins` no painel de administrador do WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="1bcf4-156">Salve as configurações de link permanente para o aplicativo WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="1bcf4-157">O último arquivo `wp-config.php`</span><span class="sxs-lookup"><span data-stu-id="1bcf4-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="1bcf4-158">As atualizações principais do WordPress não afetarão seus arquivos `wp-config.php`, `wp-config.azure.php` e `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="1bcf4-159">Aqui está uma versão final do arquivo `wp-config.php`:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-159">Here's a final version of the `wp-config.php` file:</span></span>

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="1bcf4-160">Configurar um ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="1bcf4-160">Set up a staging environment</span></span>
1. <span data-ttu-id="1bcf4-161">Se você já tiver um aplicativo Web do WordPress em execução em sua assinatura do Azure, entre no [Portal do Azure](http://portal.azure.com) e acesse seu aplicativo Web do WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="1bcf4-162">Se você não tiver um aplicativo Web do WordPress, crie um no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="1bcf4-163">Para saber mais, consulte [Criar um aplicativo Web do WordPress no Serviço de Aplicativo do Azure](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="1bcf4-164">Clique em **Configurações** > **Slots de implantação** > **Adicionar** para criar um slot de implantação com o nome *preparo*.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="1bcf4-165">Um slot de implantação é outro aplicativo Web que compartilha os mesmos recursos que o aplicativo Web principal criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Criar um slot de implantação de estágio](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="1bcf4-167">Adicione outro banco de dados MySQL, digamos `wordpress-stage-db`, ao seu grupo de recursos, `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![Adicionar banco de dados MySQL ao grupo de recursos](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="1bcf4-169">Atualize as cadeias de conexão de seu slot de implantação de preparo para apontar para o banco de dados, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="1bcf4-170">Seu aplicativo Web de produção, `wordpressprodapp` e o aplicativo Web de preparo `wordpressprodapp-stage`, têm que apontar para bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="1bcf4-171">Definir configurações específicas do ambiente de aplicativo</span><span class="sxs-lookup"><span data-stu-id="1bcf4-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="1bcf4-172">Os desenvolvedores podem armazenar pares de cadeia de chave/valor no Azure como parte das informações de configuração, chamadas de **Configurações do Aplicativo**, associadas a um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="1bcf4-173">No tempo de execução, os aplicativos Web recuperam esses valores automaticamente para você e os disponibilizam na execução do código em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="1bcf4-174">Do ponto de vista da segurança, é um bom benefício indireto, pois informações confidenciais, como cadeias de conexão de banco de dados que incluem senhas, nunca aparecem como texto não criptografado em um arquivo como o `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="1bcf4-175">Esse processo, que é explicado nos parágrafos a seguir, é útil porque inclui alterações de arquivo e alterações do banco de dados para o aplicativo do WordPress:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="1bcf4-176">Atualização de versão do WordPress</span><span class="sxs-lookup"><span data-stu-id="1bcf4-176">WordPress version upgrade</span></span>
* <span data-ttu-id="1bcf4-177">Adicionar novo, editar ou atualizar plug-ins</span><span class="sxs-lookup"><span data-stu-id="1bcf4-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="1bcf4-178">Adicionar novo, editar ou atualizar temas</span><span class="sxs-lookup"><span data-stu-id="1bcf4-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="1bcf4-179">Definir configurações do aplicativo para:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-179">Configure app settings for:</span></span>

* <span data-ttu-id="1bcf4-180">Informações de banco de dados</span><span class="sxs-lookup"><span data-stu-id="1bcf4-180">Database information</span></span>
* <span data-ttu-id="1bcf4-181">Habilitar/desabilitar o registro em log do WordPress</span><span class="sxs-lookup"><span data-stu-id="1bcf4-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="1bcf4-182">Configurações de segurança do WordPress</span><span class="sxs-lookup"><span data-stu-id="1bcf4-182">WordPress security settings</span></span>

![Configurações de Aplicativo para aplicativo Web Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="1bcf4-184">Não deixe de adicionar as seguintes configurações de aplicativo para os slots do aplicativo Web de produção e de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="1bcf4-185">Observe que os aplicativos Web de produção e de preparo usam bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="1bcf4-186">Desmarque a caixa de seleção **Configuração do Slot** para todos os parâmetros de configurações, exceto WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="1bcf4-187">Esse processo trocará a configuração de seu aplicativo Web, conteúdo do arquivo e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="1bcf4-188">Se a **Configuração de Slot** estiver marcada, as configurações de aplicativo e as configurações de cadeia de conexão do aplicativo Web *não* moverão entre ambientes durante uma operação de **Troca**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="1bcf4-189">As alterações de banco de dados presentes não interromperão o aplicativo Web de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="1bcf4-190">Implante um aplicativo Web do ambiente de desenvolvimento local no aplicativo Web de preparo e no banco de dados usando o WebMatrix, ou ferramentas de sua escolha, como FTP, Git ou PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Caixa de Diálogo Publicação do Web Matrix no aplicativo Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="1bcf4-192">Procurar e testar seu aplicativo Web de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-192">Browse and test your staging web app.</span></span> <span data-ttu-id="1bcf4-193">Considerando um cenário em que o tema do aplicativo Web deva ser atualizado, eis o aplicativo Web de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Procurar aplicativo Web de preparo antes de alternar slots](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="1bcf4-195">Se estiver tudo correto, clique no botão **Alternar** no seu aplicativo Web de preparo para mover o conteúdo para o seu ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="1bcf4-196">Neste caso, alterne o aplicativo Web e o banco de dados entre ambientes durante cada operação **Alternar** .</span><span class="sxs-lookup"><span data-stu-id="1bcf4-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Alternar alterações de visualização do WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="1bcf4-198">Se o seu cenário precisar apenas enviar arquivos por push (sem atualizações de banco de dados), verifique a **Configuração do Slot** de todas as *configurações de aplicativo* e *configurações de cadeias de conexão* relacionadas ao banco de dados na folha **Configurações do Aplicativo Web** no Portal do Azure antes de realizar a **Troca**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="1bcf4-199">Neste caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, as configurações de cadeia de conexão padrão devem aparecer nas alterações de visualização ao realizar a **Troca**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="1bcf4-200">Neste momento, quando você concluir a operação de **Troca**, o aplicativo Web do WordPress terá somente os arquivos atualizados.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="1bcf4-201">Antes de realizar uma **Troca**, este é o aplicativo Web de produção do WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="1bcf4-202">![Aplicativo Web de produção antes de trocar slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="1bcf4-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="1bcf4-203">Após a operação de **Troca**, o tema terá sido atualizado em seu aplicativo Web de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![Aplicativo Web de produção após alternar slots](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="1bcf4-205">Quando você precisar reverter, vá até as **Configurações de Aplicativo** Web de produção e clique no botão **Trocar** para trocar o aplicativo Web e o banco de dados do slot de produção para o de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="1bcf4-206">Lembre-se de que se as alterações do banco de dados estiverem incluídas em uma operação de **Troca**, na próxima vez que você implantar em seu aplicativo Web de preparo, será necessário implantar as alterações do banco de dados no banco de dados atual para seu aplicativo Web de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="1bcf4-207">O banco de dados atual pode ser o banco de dados de produção anterior ou o banco de dados de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="1bcf4-208">Resumo</span><span class="sxs-lookup"><span data-stu-id="1bcf4-208">Summary</span></span>
<span data-ttu-id="1bcf4-209">Veja a seguir um processo generalizado para qualquer aplicativo que tenha um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="1bcf4-210">Instale o aplicativo em seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="1bcf4-211">Inclua configurações específicas de ambiente (locais e Aplicativos Web do Azure).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="1bcf4-212">Configure seus ambientes de produção e preparo para aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="1bcf4-213">Se você tiver um aplicativo de produção já em execução no Azure, sincronize o conteúdo de produção (arquivos/código e banco de dados) para os ambientes de preparo e local.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="1bcf4-214">Desenvolva seu aplicativo no ambiente local.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="1bcf4-215">Coloque seu aplicativo Web de produção em manutenção ou em modo bloqueado e sincronize o conteúdo do banco de dados da produção para ambientes de teste e desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="1bcf4-216">Implante no ambiente de preparo e teste.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="1bcf4-217">Implante no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="1bcf4-218">Repita as etapas quatro a seis.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="1bcf4-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="1bcf4-219">Umbraco</span></span>
<span data-ttu-id="1bcf4-220">Nesta seção, você aprenderá como o Umbraco CMS usa um módulo personalizado para implantar em vários ambientes DevOps.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="1bcf4-221">Este exemplo fornece uma abordagem diferente para gerenciar vários ambientes de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="1bcf4-222">[Umbraco CMS](http://umbraco.com/) é uma solução de .NET CMS popular usada por muitos desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="1bcf4-223">Ela fornece o módulo [Courier2](http://umbraco.com/products/more-add-ons/courier-2) para implantar dos ambientes de desenvolvimento, passando pelo preparo até chegar à produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="1bcf4-224">Você pode criar facilmente um ambiente de desenvolvimento local para um aplicativo Web Umbraco CMS usando o Visual Studio ou o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="1bcf4-225">Criar um aplicativo Web Umbraco com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1bcf4-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="1bcf4-226">Criar um aplicativo Web Umbraco com o WebMatrix</span><span class="sxs-lookup"><span data-stu-id="1bcf4-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="1bcf4-227">Lembre-se sempre de remover a pasta `install` em seu aplicativo e nunca carregá-la em aplicativos Web em estágio ou produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="1bcf4-228">Este tutorial usa o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="1bcf4-229">Configurar um ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="1bcf4-229">Set up a staging environment</span></span>
1. <span data-ttu-id="1bcf4-230">Crie um slot de implantação, conforme mencionado anteriormente, para o aplicativo Web Umbraco CMS, supondo que você já tenha um aplicativo Web Umbraco CMS em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="1bcf4-231">Se não tiver, você poderá criar um no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="1bcf4-232">Atualize a cadeia de conexão do slot de implantação de preparo para apontar para o novo banco de dados **umbraco-stage-db**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="1bcf4-233">O aplicativo Web de produção (umbraositecms-1) e o aplicativo Web de preparo (umbracositecms-1-stage) *devem* apontar para bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Atualizar a Cadeia de conexão para aplicativos Web de preparo com o novo banco de dados de preparo](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="1bcf4-235">Clique em **Obter configurações de publicação** para o **preparo** do slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="1bcf4-236">Esse processo baixará um arquivo de configurações de publicação que armazena todas as informações exigidas pelo Visual Studio ou WebMatrix para publicar seu aplicativo do aplicativo Web de desenvolvimento local para o aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Obter configurações de publicação para o aplicativo Web de preparo](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="1bcf4-238">Abra seu aplicativo Web de desenvolvimento local no WebMatrix ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="1bcf4-239">Este tutorial usa o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="1bcf4-240">Primeiro, você precisa importar o arquivo de configurações de publicação de seu aplicativo Web de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Importar Configurações de publicação para o Umbraco usando Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="1bcf4-242">Examine as alterações feitas na caixa de diálogo e implante seu aplicativo Web local em seu aplicativo Web do Azure, *umbracositecms-1-stage*.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="1bcf4-243">Ao implantar arquivos diretamente em seu aplicativo Web de preparo, você omitirá os arquivos na pasta `~/app_data/TEMP/`, pois eles serão regenerados quando o aplicativo Web de preparo for iniciado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="1bcf4-244">Você também deverá omitir o arquivo `~/app_data/umbraco.config`, que também será regenerado.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Examinar as alterações de publicação no Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="1bcf4-246">Após a publicação bem-sucedida do aplicativo Web Umbraco local no aplicativo Web de preparo, procure seu aplicativo Web de preparo e execute alguns testes para eliminar problemas.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="1bcf4-247">Configurar módulo de implantação Courier2</span><span class="sxs-lookup"><span data-stu-id="1bcf4-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="1bcf4-248">Com o módulo [Courier2](http://umbraco.com/products/more-add-ons/courier-2), você pode simplesmente clicar com o botão direito para enviar conteúdo por push, folhas de estilo e módulos de desenvolvimento de um aplicativo Web de preparo para um aplicativo Web de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="1bcf4-249">Esse processo reduz o risco de interromper o aplicativo Web de produção ao implantar uma atualização.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="1bcf4-250">Adquira uma licença para Courier2 para o domínio `*.azurewebsites.net` e seu domínio personalizado (vamos supor http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="1bcf4-251">Após adquirir a licença, coloque a licença baixada (arquivo .LIC.) na pasta `bin`.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Soltar o arquivo de licença na pasta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="1bcf4-253">[Baixe o pacote Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="1bcf4-254">Entre no aplicativo Web de preparo, por exemplo, http://umbracocms-site-stage.azurewebsites.net/umbraco, clique no menu **Desenvolvedor** e clique em **Pacotes** > **Instalar pacote local**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Instalador do pacote Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="1bcf4-256">Carregue o pacote Courier2 usando o instalador.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-256">Upload the Courier2 package by using the installer.</span></span>

    ![Carregar pacote para módulo courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="1bcf4-258">Para configurar o pacote, você precisa atualizar o arquivo courier.config na pasta **Config** do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="1bcf4-259">Em `<repositories>`, insira a URL do site de produção e as informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="1bcf4-260">Se você estiver usando o provedor de associação Umbraco padrão, adicione a ID do usuário Administração na seção &lt;user&gt;.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="1bcf4-261">Se você estiver usando um provedor de associação do Umbraco personalizado, use `<login>` e `<password>` no módulo Courier2 para conectar-se ao site de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="1bcf4-262">Para obter mais detalhes, [confira a documentação do módulo Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="1bcf4-263">De maneira semelhante, instale o módulo Courier2 em seu site de produção e configure-o para apontar para o aplicativo Web de estágio em seu respectivo arquivo courier.config, conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="1bcf4-264">Clique na guia **Courier2** no painel do aplicativo Web Umbraco CMS e clique em **Locais**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="1bcf4-265">Você deve ver o nome do repositório, como mencionado em `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="1bcf4-266">Faça esse processo em seus aplicativos Web de preparo e de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-266">Do this process on both your production and staging web apps.</span></span>

    ![Exibir repositório de aplicativo Web de destino](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="1bcf4-268">Para implantar o conteúdo do site de preparo para o site de produção, acesse **Conteúdo** e selecione uma página existente ou crie uma nova página.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="1bcf4-269">Selecionarei uma página existente de meu aplicativo Web cujo título da página é **Introdução – novo** e clicarei em **Salvar e Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Alterar o título da página e publicar](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="1bcf4-271">Clique com o botão direito do mouse na página modificada para exibir todas as opções.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="1bcf4-272">Clique em **Courier** para abrir a caixa de diálogo **Implantação**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="1bcf4-273">Clique em **Implantar** para iniciar a implantação.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-273">Click **Deploy** to initiate deployment.</span></span>

    ![Diálogo de implantação de módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="1bcf4-275">Analise as alterações e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-275">Review the changes, and then click **Continue**.</span></span>

    ![Alterações de análise do diálogo de implantação de módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="1bcf4-277">O log de implantação mostra se a implantação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-277">The deployment log shows if the deployment was successful.</span></span>

     ![Exibir Logs de implantação do módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="1bcf4-279">Procure seu aplicativo Web de produção para ver se as alterações foram reproduzidas.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Procurar o aplicativo Web de produção](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="1bcf4-281">Para saber mais sobre como usar o Courier, leia a documentação.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="1bcf4-282">Como atualizar a versão CMS do Umbraco</span><span class="sxs-lookup"><span data-stu-id="1bcf4-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="1bcf4-283">O Courier não ajudará com a atualização de uma versão do Umbraco CMS para outra.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="1bcf4-284">Ao atualizar a versão CMS do Umbraco, você deve verificar as incompatibilidades entre seus módulos personalizados ou módulos de parceiros e as bibliotecas principais do Umbraco.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="1bcf4-285">Estas são as práticas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-285">Here are best practices:</span></span>

* <span data-ttu-id="1bcf4-286">Sempre faça backup de seu aplicativo Web e do banco de dados antes de fazer uma atualização.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="1bcf4-287">Em aplicativos Web no Azure, você pode configurar backups automáticos para seus sites usando o recurso de backup e restaurando seu site, se for necessário, usando o recurso restaurar.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="1bcf4-288">Para obter mais detalhes, veja [Como fazer backup de seu aplicativo Web](web-sites-backup.md) e [Como restaurar seu aplicativo Web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="1bcf4-289">Verifique se os pacotes de parceiros são compatíveis com a versão para a qual você está atualizando.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="1bcf4-290">Na página de download do pacote, examine a compatibilidade de projeto com a versão do Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="1bcf4-291">Para obter mais detalhes sobre como atualizar seu aplicativo Web localmente, [consulte o guia de atualização geral](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="1bcf4-292">Após a atualização do site de desenvolvimento local, publique as alterações no aplicativo Web de preparo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="1bcf4-293">Teste seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-293">Test your application.</span></span> <span data-ttu-id="1bcf4-294">Se estiver tudo certo, use o botão **Trocar** para trocar seu site de preparo para o aplicativo Web de produção.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="1bcf4-295">Ao usar a operação **Trocar**, você poderá exibir as alterações que serão afetadas na configuração de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="1bcf4-296">Essa operação de **Troca** alterna os bancos de dados e aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="1bcf4-297">Após a **Troca**, o aplicativo Web de produção apontará para o banco de dados umbraco-stage-db, e o aplicativo Web de preparo apontará para o banco de dados umbraco-prod-db.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Alternar visualização para implantar o Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="1bcf4-299">Estas são as vantagens de trocar o aplicativo Web e o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="1bcf4-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="1bcf4-300">Você pode reverter para a versão anterior do seu aplicativo Web com outra **Troca** se houver algum problema com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="1bcf4-301">Para uma atualização, você precisa implantar arquivos e banco de dados do aplicativo Web de preparo para o aplicativo Web de produção e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="1bcf4-302">Muitas coisas que podem dar errado quando você implanta arquivos e bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="1bcf4-303">Usando o recurso **Troca** dos slots, podemos reduzir o tempo de inatividade durante uma atualização e reduzir o risco de falhas que podem ocorrer na implantação das alterações.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="1bcf4-304">Você pode fazer o **Teste A/B** usando o recurso [Teste em produção](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/).</span><span class="sxs-lookup"><span data-stu-id="1bcf4-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="1bcf4-305">Este exemplo mostra a flexibilidade da plataforma, onde você pode criar módulos personalizados semelhantes ao módulo Umbraco Courier para gerenciar a implantação entre ambientes.</span><span class="sxs-lookup"><span data-stu-id="1bcf4-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="1bcf4-306">Referências</span><span class="sxs-lookup"><span data-stu-id="1bcf4-306">References</span></span>
[<span data-ttu-id="1bcf4-307">Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="1bcf4-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="1bcf4-308">Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="1bcf4-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="1bcf4-309">Como bloquear acesso via Web a slots de implantação de não produção</span><span class="sxs-lookup"><span data-stu-id="1bcf4-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
