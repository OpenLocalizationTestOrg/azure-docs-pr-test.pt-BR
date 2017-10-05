---
title: "Converter WordPress em Multissite no Serviço de Aplicativo do Azure"
description: "Saiba como selecionar um aplicativo Web WordPress existente criado por meio da galeria no Azure e convertê-lo em Multissite WordPress"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="d8166-103">Converter WordPress em Multissite no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="d8166-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="d8166-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d8166-104">Overview</span></span>
<span data-ttu-id="d8166-105">*Por [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="d8166-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="d8166-106">Neste tutorial, você aprenderá converter um aplicativo Web do WordPress criado por meio da galeria no Azure em uma instalação multissite do WordPress.</span><span class="sxs-lookup"><span data-stu-id="d8166-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="d8166-107">Além disso, você aprenderá a atribuir um domínio personalizado para cada um dos subsites dentro de sua instalação.</span><span class="sxs-lookup"><span data-stu-id="d8166-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="d8166-108">Presume-se que você tem uma instalação existente do WordPress.</span><span class="sxs-lookup"><span data-stu-id="d8166-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="d8166-109">Se você não fizer isso, siga as orientações apresentadas no [criar um site do WordPress da galeria no Azure][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="d8166-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="d8166-110">Convertendo um WordPress existente instalar único site multissite geralmente é bastante simple e muitas das etapas iniciais são provenientes diretamente o [Criar uma rede][wordpress-codex-create-a-network] página no [WordPress Codex](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="d8166-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="d8166-111">Vamos começar.</span><span class="sxs-lookup"><span data-stu-id="d8166-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="d8166-112">Permitir que o multissite</span><span class="sxs-lookup"><span data-stu-id="d8166-112">Allow Multisite</span></span>
<span data-ttu-id="d8166-113">Primeiro você precisa habilitar o Multissite por meio do arquivo `wp-config.php` com a constante **WP\_ALLOW\_MULTISITE**.</span><span class="sxs-lookup"><span data-stu-id="d8166-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="d8166-114">Há dois métodos para editar os arquivos do seu aplicativo Web: a primeira é por meio de FTP e o segundo é por meio do Git.</span><span class="sxs-lookup"><span data-stu-id="d8166-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="d8166-115">Se você não estiver familiarizado com a instalação de qualquer um desses métodos, consulte os seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="d8166-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="d8166-116">[Site do PHP com o MySQL e FTP][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="d8166-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="d8166-117">[Site do PHP com o MySQL e Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="d8166-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="d8166-118">Abra o arquivo `wp-config.php` com o editor da sua escolha e adicione o seguinte acima da linha `/* That's all, stop editing! Happy blogging. */`.</span><span class="sxs-lookup"><span data-stu-id="d8166-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="d8166-119">Certifique-se de salvá-lo e carregá-lo de volta para o servidor!</span><span class="sxs-lookup"><span data-stu-id="d8166-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="d8166-120">Configuração de rede</span><span class="sxs-lookup"><span data-stu-id="d8166-120">Network Setup</span></span>
<span data-ttu-id="d8166-121">Faça logon na área *wp-admin* de seu aplicativo Web e você verá um novo item no menu **Ferramentas**, chamado **Configuração de Rede**.</span><span class="sxs-lookup"><span data-stu-id="d8166-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="d8166-122">Clique em **o programa de instalação de rede** e preencha os detalhes da sua rede.</span><span class="sxs-lookup"><span data-stu-id="d8166-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Tela de configuração de rede][wordpress-network-setup]

<span data-ttu-id="d8166-124">Este tutorial usa a *subdiretórios* site esquema porque ele sempre deve funcionar, e vão configurar domínios personalizados para cada subsite posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="d8166-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="d8166-125">No entanto, deve ser possível configurar uma instalação de subdomínio se você mapear adequadamente um domínio por meio do [Portal do Azure](https://portal.azure.com) e do DNS curinga de configuração.</span><span class="sxs-lookup"><span data-stu-id="d8166-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="d8166-126">Para obter mais informações sobre o subdomínio vs subpasta configurações Consulte o [Tipos de rede multissite][wordpress-codex-types-of-networks] artigo sobre o WordPress Codex.</span><span class="sxs-lookup"><span data-stu-id="d8166-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="d8166-127">Ativar a rede</span><span class="sxs-lookup"><span data-stu-id="d8166-127">Enable the Network</span></span>
<span data-ttu-id="d8166-128">A rede agora está configurada no banco de dados, mas há uma etapa restante para habilitar a funcionalidade de rede.</span><span class="sxs-lookup"><span data-stu-id="d8166-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="d8166-129">Finalize as configurações `wp-config.php` e verifique se `web.config` roteia corretamente cada site.</span><span class="sxs-lookup"><span data-stu-id="d8166-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="d8166-130">Depois que você clicar no botão **Instalar** na página *Configuração de Rede*, o WordPress tentará atualizar os arquivos `wp-config.php` e `web.config`.</span><span class="sxs-lookup"><span data-stu-id="d8166-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="d8166-131">No entanto, você sempre deve verificar os arquivos para garantir que as atualizações foram bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="d8166-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="d8166-132">Caso contrário, esta tela apresentará as atualizações necessárias.</span><span class="sxs-lookup"><span data-stu-id="d8166-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="d8166-133">Editar e salvar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="d8166-133">Edit and save the files.</span></span>

<span data-ttu-id="d8166-134">Depois de fazer essas atualizações, você precisará fazer logoff e depois fazer logon no painel wp-admin.</span><span class="sxs-lookup"><span data-stu-id="d8166-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="d8166-135">Agora deve haver um menu adicional na barra de administrador com o rótulo **Meus Sites**.</span><span class="sxs-lookup"><span data-stu-id="d8166-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="d8166-136">Esse menu permite que você controle sua nova rede através do painel **Administrador de rede**.</span><span class="sxs-lookup"><span data-stu-id="d8166-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="d8166-137">Adicionando domínios personalizados</span><span class="sxs-lookup"><span data-stu-id="d8166-137">Adding custom domains</span></span>
<span data-ttu-id="d8166-138">O [Mapeamento de domínio do WordPress MU][wordpress-plugin-wordpress-mu-domain-mapping] plug-in facilita adicionar domínios personalizados para qualquer site na sua rede.</span><span class="sxs-lookup"><span data-stu-id="d8166-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="d8166-139">O plug-in funcionar corretamente, é necessário fazer algumas configurações adicionais no Portal e também em seu registrador de domínio.</span><span class="sxs-lookup"><span data-stu-id="d8166-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="d8166-140">Habilitar o mapeamento de domínio para o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d8166-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="d8166-141">O **Gratuito** [Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) não dá suporte a adição de domínios personalizados para aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="d8166-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="d8166-142">Você precisará mudar para o modo **Compartilhado** ou **Padrão**.</span><span class="sxs-lookup"><span data-stu-id="d8166-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="d8166-143">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="d8166-143">To do this:</span></span>

* <span data-ttu-id="d8166-144">Faça logon no Portal do Azure e localize seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d8166-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="d8166-145">Clique na guia **Escalar verticalmente** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="d8166-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="d8166-146">Em **Geral**, selecione *COMPARTILHADO* ou *STANDARD*</span><span class="sxs-lookup"><span data-stu-id="d8166-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="d8166-147">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="d8166-147">Click **Save**</span></span>

<span data-ttu-id="d8166-148">Você pode receber uma mensagem pedindo-lhe para verificar a alteração e confirmar que o seu aplicativo Web agora pode incorrer em custos, dependendo do uso e de outras configurações definidas por você.</span><span class="sxs-lookup"><span data-stu-id="d8166-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="d8166-149">Demora alguns segundos para processar as novas configurações, agora é um bom momento para iniciar a configuração do domínio.</span><span class="sxs-lookup"><span data-stu-id="d8166-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="d8166-150">Verifique se seu domínio</span><span class="sxs-lookup"><span data-stu-id="d8166-150">Verify your domain</span></span>
<span data-ttu-id="d8166-151">Para que os Aplicativos Web do Azure lhe permitam mapear um domínio para o site, primeiro você precisa verificar se tem autorização para mapear tal domínio.</span><span class="sxs-lookup"><span data-stu-id="d8166-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="d8166-152">Para fazer isso, você deve adicionar um novo registro CNAME para sua entrada DNS.</span><span class="sxs-lookup"><span data-stu-id="d8166-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="d8166-153">Efetuar login no Gerenciador de DNS do seu domínio</span><span class="sxs-lookup"><span data-stu-id="d8166-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="d8166-154">Criar um novo CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="d8166-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="d8166-155">Aponte o *awverify* para *awverify.YOUR_DOMAIN.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="d8166-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="d8166-156">Levará algum tempo para que as alterações DNS entrar em vigor, portanto, se estas etapas não funcionar imediatamente, uma xícara de café, e em seguida, volte e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="d8166-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="d8166-157">Adicionar o nome de domínio ao aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d8166-157">Add the domain to the web app</span></span>
<span data-ttu-id="d8166-158">Voltar ao seu aplicativo Web por meio do Portal do Azure, clique em **Configurações** e, em seguida, clique em **Domínios personalizados e SSL**.</span><span class="sxs-lookup"><span data-stu-id="d8166-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="d8166-159">Quando as *Configurações de SSL* forem exibidas, você verá os campos onde digitará todos os domínios que você deseja atribuir ao seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d8166-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="d8166-160">Se um domínio não estiver listado aqui, ela não estará disponível para mapeamento dentro de WordPress, independentemente de como o domínio DNS é o programa de instalação.</span><span class="sxs-lookup"><span data-stu-id="d8166-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Caixa de diálogo domínios personalizados gerenciar][wordpress-manage-domains]

<span data-ttu-id="d8166-162">Depois de digitar seu domínio na caixa de texto, o Azure verificará o registro CNAME que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d8166-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="d8166-163">Se o DNS não tiver sido propagado totalmente, um indicador vermelho será exibido.</span><span class="sxs-lookup"><span data-stu-id="d8166-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="d8166-164">Se tiver êxito, você verá uma marca de seleção verde.</span><span class="sxs-lookup"><span data-stu-id="d8166-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="d8166-165">Anote o endereço IP listado na parte inferior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d8166-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="d8166-166">Será necessário configurar o registro para o seu domínio.</span><span class="sxs-lookup"><span data-stu-id="d8166-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="d8166-167">Configurar o domínio de um registro</span><span class="sxs-lookup"><span data-stu-id="d8166-167">Setup the domain A record</span></span>
<span data-ttu-id="d8166-168">Se as outras etapas forem bem-sucedidas, agora você pode atribuir o domínio a seu aplicativo Web do Azure por meio de um registro A DNS.</span><span class="sxs-lookup"><span data-stu-id="d8166-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="d8166-169">É importante observar aqui que aplicativos Web do Azure aceitam registros CNAME e A; no entanto, você *deve* usar um registro para habilitar o mapeamento de domínio correto.</span><span class="sxs-lookup"><span data-stu-id="d8166-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="d8166-170">Um CNAME não pode ser encaminhado para outro CNAME, que é o Azure criada para você com YOUR_DOMAIN.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="d8166-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="d8166-171">Usando o endereço IP da etapa anterior, volte para o Gerenciador de DNS e configurar o registro para apontar para esse IP.</span><span class="sxs-lookup"><span data-stu-id="d8166-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="d8166-172">Instalar e configurar o plug-in</span><span class="sxs-lookup"><span data-stu-id="d8166-172">Install and setup the plugin</span></span>
<span data-ttu-id="d8166-173">Atualmente, o multissite do WordPress não tem um método interno para mapear domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="d8166-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="d8166-174">No entanto, há um plug-in chamado [Mapeamento de domínio do WordPress MU][wordpress-plugin-wordpress-mu-domain-mapping] que adiciona a funcionalidade para você.</span><span class="sxs-lookup"><span data-stu-id="d8166-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="d8166-175">Login à parte de seu site do administrador de rede e instalar o **mapeamento de domínio do WordPress MU** plug-in.</span><span class="sxs-lookup"><span data-stu-id="d8166-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="d8166-176">Após instalar e ativar o plug-in, visite **Configurações** > **mapeamento de domínio** para configurar o plug-in.</span><span class="sxs-lookup"><span data-stu-id="d8166-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="d8166-177">Na primeira caixa de texto, *endereço IP do servidor*, insira o endereço de IP é usada para configurar o registro para o domínio.</span><span class="sxs-lookup"><span data-stu-id="d8166-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="d8166-178">Defina qualquer *opções de domínio* você desejo (os padrões geralmente são bem) e clique em **salvar**</span><span class="sxs-lookup"><span data-stu-id="d8166-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="d8166-179">Mapa de domínio</span><span class="sxs-lookup"><span data-stu-id="d8166-179">Map the domain</span></span>
<span data-ttu-id="d8166-180">Visite o **painel** para o site que deseja mapear o domínio.</span><span class="sxs-lookup"><span data-stu-id="d8166-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="d8166-181">Clique em **Ferramentas** > **Mapeamento de domínio** e digite o novo domínio na caixa de texto e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d8166-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="d8166-182">Por padrão, o novo domínio será regravado no domínio do site gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d8166-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="d8166-183">Se você deseja ter todo o tráfego enviado para o novo domínio, seleção de *o domínio primário para este blog* caixa antes de salvar.</span><span class="sxs-lookup"><span data-stu-id="d8166-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="d8166-184">Você pode adicionar um número ilimitado de domínios em um site, mas apenas um pode ser o principal.</span><span class="sxs-lookup"><span data-stu-id="d8166-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="d8166-185">Fazê-lo novamente</span><span class="sxs-lookup"><span data-stu-id="d8166-185">Do it again</span></span>
<span data-ttu-id="d8166-186">Aplicativos Web do Azure permitem que você adicione um número ilimitado de domínios a um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d8166-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="d8166-187">Para adicionar outro domínio, você precisará executar as seções **Verifique se seu domínio** e **Configurar registro do domínio A** para cada domínio.</span><span class="sxs-lookup"><span data-stu-id="d8166-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="d8166-188">Se você deseja começar a usar o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8166-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d8166-189">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="d8166-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="d8166-190">O que mudou</span><span class="sxs-lookup"><span data-stu-id="d8166-190">What's changed</span></span>
* <span data-ttu-id="d8166-191">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d8166-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


