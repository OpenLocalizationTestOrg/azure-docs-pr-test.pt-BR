---
title: "O que há de novo no gerenciamento de aplicativos empresariais no Azure Active Directory | Microsoft Docs"
description: "Saiba o que há de novo no gerenciamento de aplicativos empresariais no Azure Active Directory."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: asteen
ms.reviewer: asteen
ms.openlocfilehash: 0c32a6719292aa903aa32dfdc4a31114e7a28346
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="whats-new-in-enterprise-application-management-in-azure-active-directory"></a><span data-ttu-id="d4143-103">O que há de novo no gerenciamento de aplicativos empresariais no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4143-103">What's new in Enterprise Application management in Azure Active Directory</span></span> 

<span data-ttu-id="d4143-104">O Azure AD (Azure Active Directory) aprimorou as ferramentas de gerenciamento de aplicativos empresariais, com novos recursos e funcionalidades para tornar os aplicativos de gerenciamento mais simples e eficientes.</span><span class="sxs-lookup"><span data-stu-id="d4143-104">Azure Active Directory (Azure AD) has enhanced enterprise application management tools, with new features and capabilities to make managing apps simpler and efficient.</span></span>

<span data-ttu-id="d4143-105">A seguir estão alguns dos aprimoramentos do Azure AD no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4143-105">Following are some of the enhancements for Azure AD in the [Azure portal](https://portal.azure.com).</span></span>

- <span data-ttu-id="d4143-106">Uma experiência aprimorada da galeria de aplicativos, com um modelo de criação de aplicativos simplificado e suporte para todos os tipos de aplicativo aos quais você está acostumado.</span><span class="sxs-lookup"><span data-stu-id="d4143-106">An improved application gallery experience, with a simplified application creation model and support for all the application types that you’re used to.</span></span> 
- <span data-ttu-id="d4143-107">Uma experiência de início rápido totalmente nova, que lhe ajuda a começar com um piloto do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-107">A brand-new quick start experience that can help you get going with a pilot of your application.</span></span> 
- <span data-ttu-id="d4143-108">Configure as políticas de autoatendimento com apenas alguns cliques.</span><span class="sxs-lookup"><span data-stu-id="d4143-108">Configure self-service policies with just a few clicks.</span></span> 
- <span data-ttu-id="d4143-109">Melhorias significativas no proxy de aplicativo, na configuração de logon único e nas experiências de trazer seu próprio aplicativo, permitindo que você faça mais do que antes.</span><span class="sxs-lookup"><span data-stu-id="d4143-109">Improvements to application proxy, single sign-on configuration, and bring your own application experiences, allowing you to get more done than before.</span></span>

## <a name="improvements-to-the-azure-active-directory-application-gallery"></a><span data-ttu-id="d4143-110">Melhorias à Galeria de Aplicativos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4143-110">Improvements to the Azure Active Directory Application Gallery</span></span>

<span data-ttu-id="d4143-111">Adicione seus aplicativos favoritos, sejam eles da [galeria de aplicativos](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), aplicativos personalizados que você está estendendo para a nuvem ou novos aplicativos que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="d4143-111">Add your favorite applications whether they are from the [application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), custom applications you’re extending to the cloud, or new applications you’re developing.</span></span>  <span data-ttu-id="d4143-112">Você pode começar com esta nova experiência clicando em **Adicionar** nas folhas da visão geral dos **Aplicativos Empresariais** ou **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d4143-112">You can get started with this new experience by clicking **Add** on the **Enterprise Applications** overview or **All applications** blades.</span></span>
 
  ![Adicionando um aplicativo](./media/active-directory-enterprise-apps-whats-new-azure-portal/01.png)

<span data-ttu-id="d4143-114">Uma vez na galeria, você verá todos os nossos aplicativos em destaque, o que auxilia no provisionamento do usuário com sua exibição na frente e no centro.</span><span class="sxs-lookup"><span data-stu-id="d4143-114">Once in the gallery, you’ll see all our featured applications which support user provisioning displayed front-and-center.</span></span>  <span data-ttu-id="d4143-115">Você pode procurar todos os tipos de categorias diferentes para detalhar os aplicativos importantes, ou pode usar a experiência de pesquisa para localizar rapidamente os aplicativos que você deseja integrar.</span><span class="sxs-lookup"><span data-stu-id="d4143-115">You can browse all sorts of different categories to drill into the applications you care about, or you can use the search experience to rapidly find the applications you want to integrate.</span></span>

  ![A galeria de aplicativos](./media/active-directory-enterprise-apps-whats-new-azure-portal/02.png)

## <a name="add-custom-applications-from-one-place"></a><span data-ttu-id="d4143-117">Adicionar aplicativos personalizados de um só lugar</span><span class="sxs-lookup"><span data-stu-id="d4143-117">Add custom applications from one place</span></span>

<span data-ttu-id="d4143-118">Além de adicionar aplicativos pré-integrados da galeria, todas as experiências de configuração do aplicativo personalizado que você já conhece do portal de gerenciamento clássico agora são possíveis no novo portal.</span><span class="sxs-lookup"><span data-stu-id="d4143-118">In addition to adding pre-integrated applications from the gallery, all the custom application configuration experiences that you were used to in the classic management portal are now possible in the new portal.</span></span> <span data-ttu-id="d4143-119">Se você estiver estendendo um aplicativo no local usando o proxy de aplicativo, integrando sua própria senha ou aplicativo SSO federado, ou criando um aplicativo totalmente novo usando o registro do aplicativo, tudo isso poderá ser feito nesse único local.</span><span class="sxs-lookup"><span data-stu-id="d4143-119">Whether you are extending an application from on-premises using the application proxy, integrating your own password or federated SSO application, or creating a brand-new application using the application registry, you can get to it all from this one single place.</span></span>

  ![Adicionar seu próprio aplicativo](./media/active-directory-enterprise-apps-whats-new-azure-portal/03.png)

 
<span data-ttu-id="d4143-121">**Para começar a adicionar seu próprio aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="d4143-121">**To get started adding your own application**:</span></span>

1. <span data-ttu-id="d4143-122">Clique no **link adicionar seu próprio** na parte superior da galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d4143-122">Click the **add your own link** at the top of the application gallery.</span></span> 
2. <span data-ttu-id="d4143-123">Você verá duas opções na sua frente: **implantar um aplicativo existente** ou **desenvolver um novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d4143-123">You’ll see two options in front of you: **deploy an existing application** or **develop a new application**.</span></span> <span data-ttu-id="d4143-124">Continue lendo para saber a diferença entre as duas opções e como usá-las.</span><span class="sxs-lookup"><span data-stu-id="d4143-124">Read on to learn the difference between the two options and how to use them.</span></span>

### <a name="deploying-existing-applications"></a><span data-ttu-id="d4143-125">Implantação de aplicativos existentes</span><span class="sxs-lookup"><span data-stu-id="d4143-125">Deploying existing applications</span></span>

1. <span data-ttu-id="d4143-126">Se você já tiver um aplicativo em execução e deseja apenas para integrá-lo ao Azure AD para logon único ou provisionamento, escolha a opção **Implantar um aplicativo existente**.</span><span class="sxs-lookup"><span data-stu-id="d4143-126">If you’ve got an application running already and just want to integrate it into Azure AD for single-sign on or provisioning, choose the **Deploy an existing application** option.</span></span> <span data-ttu-id="d4143-127">Escolha um nome para seu aplicativo, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4143-127">Pick a name for your application, click **Add**.</span></span>
2. <span data-ttu-id="d4143-128">É isso!</span><span class="sxs-lookup"><span data-stu-id="d4143-128">That's it!</span></span> <span data-ttu-id="d4143-129">Em vez de precisar saber todos os detalhes sobre seu aplicativo com antecedência, você pode definir o funcionamento do seu novo aplicativo navegando por meio do menu à esquerda e configurar o aplicativo de sua preferência a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="d4143-129">Instead of needing to know all the details about your application up front, you can now set up how your new application works by navigating through the left menu and configuring the application to your liking at any time.</span></span>

  ![Adicionar um aplicativo existente com um clique](./media/active-directory-enterprise-apps-whats-new-azure-portal/04.png)
 
### <a name="developing-new-applications"></a><span data-ttu-id="d4143-131">Desenvolver novos aplicativos</span><span class="sxs-lookup"><span data-stu-id="d4143-131">Developing new applications</span></span>

1. <span data-ttu-id="d4143-132">Se você estiver desenvolvendo um novo aplicativo, há uma maneira fácil de acessar o Registro de Aplicativo à direita da galeria:</span><span class="sxs-lookup"><span data-stu-id="d4143-132">If you’re developing a new application, there's an easy way for you to get to the Application Registry right from the gallery:</span></span>
2. <span data-ttu-id="d4143-133">Clique na opção **adicionar seu próprio** na Galeria de Aplicativos, selecione a opção **desenvolver um aplicativo existente** e você verá um link à direita para a experiência de adição de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-133">Click on the **add your own** option from the Application Gallery, select the **develop an existing application** choice, and you’ll see a quick link right to the application add experience.</span></span>

  ![Adicionar um aplicativo recém-desenvolvido em alguns cliques](./media/active-directory-enterprise-apps-whats-new-azure-portal/05.png)


>[!NOTE]
><span data-ttu-id="d4143-135">Depois de adicionar um aplicativo usando o Registro de Aplicativo, ele será mostrado na lista de Aplicativos Empresariais, onde você poderá configurar o logon único e gerenciar políticas de acesso para o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-135">Once you add an application using the Application Registry, you’ll see it show up in the list of Enterprise Applications where you’ll be able to configure single sign-on and manage access policies for your new application.</span></span>

  ![Gerenciamento do acesso a seu novo aplicativo em Aplicativos Empresariais](./media/active-directory-enterprise-apps-whats-new-azure-portal/06.png)


## <a name="quick-start-get-going-with-your-new-application-right-away"></a><span data-ttu-id="d4143-137">Início rápido: Começar a usar seu novo aplicativo imediatamente</span><span class="sxs-lookup"><span data-stu-id="d4143-137">Quick start: Get going with your new application right away</span></span> 

<span data-ttu-id="d4143-138">Depois de adicionar um aplicativo, independentemente de ser pré-integrado ou seu próprio aplicativo, criamos uma experiência personalizada de início rápido para ajudá-lo a começar a usar rapidamente o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-138">After you’ve added an application, whether it be pre-integrated or your own app, we’ve created a tailored quick-start experience to get you grounded in the new applications experience quickly.</span></span> <span data-ttu-id="d4143-139">Se você seguir sistematicamente cada opção, vamos conduzi-lo por meio da interface do isuário e mostraremos como começar com um piloto do seu novo aplicativo o mais rápido possível.</span><span class="sxs-lookup"><span data-stu-id="d4143-139">If you follow each option systematically, we’ll walk you through the UI and show you how to get going with a pilot of your new application as quickly as possible.</span></span> 
 
  ![Experiência de início rápido de novos aplicativos](./media/active-directory-enterprise-apps-whats-new-azure-portal/07.png)

 <span data-ttu-id="d4143-141">Você pode visitar esta nova experiência de início rápido, a qualquer momento e de qualquer aplicativo, clicando em **Início rápido** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-141">You can visit this new quick start experience at any time, and for any application, by clicking on **Quick start** from the application left navigation menu.</span></span>


## <a name="updated-application-proxy-configuration"></a><span data-ttu-id="d4143-142">Configuração de proxy de aplicativo atualizada</span><span class="sxs-lookup"><span data-stu-id="d4143-142">Updated application proxy configuration</span></span>
<span data-ttu-id="d4143-143">Agora, digamos que um dos novos aplicativos que você adicionou esteja em execução no seu ambiente local e você deseja integrá-lo ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4143-143">Now, let’s say one of the new applications you added is running in your on-premises environment and you want to integrate it with Azure AD.</span></span>  <span data-ttu-id="d4143-144">Uma das novidades interessantes sobre a nova experiência de configuração de aplicativo no novo portal do Azure AD é que ao dividir o modo de logon do aplicativo da configuração de proxy de aplicativo, agora você pode facilmente expor os aplicativos de SSO com senha ou federados executados em sua rede corporativa diretamente na nuvem, sem a necessidade de criar várias instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-144">One of the cool new things about the new application configuration experience in the new Azure AD portal is that by splitting the application’s sign-on mode from its application proxy configuration, you can now easily expose password SSO or federated applications that are running in your corporate network right to the cloud, without having to create multiple instances of the application.</span></span>

<span data-ttu-id="d4143-145">Além disso, agora também é possível configurar qualquer um dos novos aplicativos que você adicionou para uso com o direito de Proxy de Aplicativo do Azure AD do novo portal, incluindo os aplicativos que oferecem suporte a experiências nativas de autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="d4143-145">In addition to this, you can now also configure any of the new applications you’ve added for use with the Azure AD Application Proxy right from the new portal, including applications which support native Windows authentication experiences.</span></span>

  ![Configurar um aplicativo para usar a opção de logon de Autenticação Integrada do Windows](./media/active-directory-enterprise-apps-whats-new-azure-portal/08.png)
 

<span data-ttu-id="d4143-147">Para começar a configurar um aplicativo nativo de autenticação do Windows com o Proxy de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d4143-147">To get started configuring a native Windows authentication application with the Application Proxy:</span></span>
1. <span data-ttu-id="d4143-148">Clique no item de navegação Logon Único e escolha **Autenticação Integrada do Windows** da folha configurações de logon e defina as configurações de sua preferência.</span><span class="sxs-lookup"><span data-stu-id="d4143-148">Click on the Single sign-on navigation item and choose **Integrated Windows Authentication** from the sign-on settings blade and configure the settings to your liking.</span></span>
2. <span data-ttu-id="d4143-149">Sobre o suporte a esses novos modos de autenticação, agora você pode também carregar certificados de domínios personalizados para oferecer suporte a aplicativos executados em pontos de extremidade seguros dentro da sua organização.</span><span class="sxs-lookup"><span data-stu-id="d4143-149">On top of supporting these new authentication modes, you can now also upload certificates from custom domains to support applications running on secure endpoints within your organization.</span></span>  
 
   ![Carregar um certificado a ser usado com o Proxy de Aplicativo](./media/active-directory-enterprise-apps-whats-new-azure-portal/09.png)

3. <span data-ttu-id="d4143-151">Para carregar um novo certificado para o seu aplicativo local favorito, clique na opção **Proxy de aplicativo** no menu de navegação à esquerda, clique no seletor **Certificado** e carregue um arquivo de certificado que podemos usar para criptografar solicitações de nosso ponto de extremidade de nuvem para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-151">To upload a new certificate for your favorite on-premises application, click on the **Application proxy** option from the left navigation menu, click the **Certificate** selector, and upload a certificate file we can use to encrypt requests from our cloud endpoint to your application.</span></span>

## <a name="advanced-federated-single-sign-on-configuration"></a><span data-ttu-id="d4143-152">Configuração avançada de logon único federado</span><span class="sxs-lookup"><span data-stu-id="d4143-152">Advanced federated single sign-on configuration</span></span>

<span data-ttu-id="d4143-153">Para aqueles que utilizam aplicativos federados hoje, há muitos novos recursos na folha de configuração de logon único baseado em SAML.</span><span class="sxs-lookup"><span data-stu-id="d4143-153">For those of you using federated applications today, there are many new features in the SAML-based sign-on configuration blade.</span></span> <span data-ttu-id="d4143-154">Para começar, agora você pode personalizar, adicionar, remover e mapear totalmente os atributos de usuário existentes emitidos como declarações em tokens SAML.</span><span class="sxs-lookup"><span data-stu-id="d4143-154">To start with, now you can fully customize, add, remove, and map the existing user attributes issued as claims in SAML tokens.</span></span>
 
  ![Personalizar os atributos de usuário do token SAML passado para um aplicativo federado](./media/active-directory-enterprise-apps-whats-new-azure-portal/10.png)


<span data-ttu-id="d4143-156">Para conferir a nova configuração de SSO federado:</span><span class="sxs-lookup"><span data-stu-id="d4143-156">To check that out the new federated SSO configuration:</span></span>
1. <span data-ttu-id="d4143-157">Abra a folha **logon único** de um aplicativo federado no menu de navegação esquerdo e verifique se o modo '*Logon Único Baseado em SAML** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="d4143-157">Open a federated application’s **single sign-on** blade from the left navigation menu and make sure the ‘*SAML-based Sign-on** mode is selected.</span></span> 
2. <span data-ttu-id="d4143-158">Uma vez lá, habilite a caixa de seleção no título **Atributos de Usuário** para modificar todos os atributos incluídos no token SAML passado para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-158">Once there, enable the checkbox under the **User Attributes** heading to modify all of the attributes included in the SAML token passed to that application.</span></span>

<span data-ttu-id="d4143-159">Você pode também criar, substituir e gerenciar os certificados usados para logon único federado, bem como editar quem será notificado quando o certificado estiver prestes a expirar.</span><span class="sxs-lookup"><span data-stu-id="d4143-159">You can also create, rollover, and manage certificates used for federated single sign-on, as well as edit who gets notified when your certificate is about to expire.</span></span> <span data-ttu-id="d4143-160">Você verá essas novas opções no título **Certificados** na mesma folha Logon único.</span><span class="sxs-lookup"><span data-stu-id="d4143-160">You’ll see these new options under the **Certificates** heading on the same Single sign-on blade.</span></span>
 
  ![Criar um novo certificado, personalizando o email de notificação de expiração e opções de assinatura de certificado](./media/active-directory-enterprise-apps-whats-new-azure-portal/11.png)

### <a name="relay-state-paramenter"></a><span data-ttu-id="d4143-162">Parâmetro de estado de retransmissão</span><span class="sxs-lookup"><span data-stu-id="d4143-162">Relay State paramenter</span></span>
<span data-ttu-id="d4143-163">Por fim, também ampliamos o conjunto de parâmetros de URL do SAML, oferecemos suporte para incluir o **parâmetro Estado de Retransmissão**, que é a página em que os usuários aterrissarão em um aplicativo federado depois que a entrada for concluída.</span><span class="sxs-lookup"><span data-stu-id="d4143-163">Finally, we’ve also extended the set of SAML URL parameters we support to include the **Relay State parameter**, which is the page your users will land on inside of a federated application once the sign-in is completed.</span></span> <span data-ttu-id="d4143-164">Essa é uma configuração muito útil para configurar se deseja enviar os usuários para um local específico dentro do aplicativo para que eles comecem a usar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="d4143-164">This is very useful setting to configure if you want to send your users to a specific place within the application to get them going quickly.</span></span>

  ![Definição do parâmetro Estado de Retransmissão de SAML](./media/active-directory-enterprise-apps-whats-new-azure-portal/12.png)
 
<span data-ttu-id="d4143-166">**Para definir o parâmetro de estado de retransmissão**:</span><span class="sxs-lookup"><span data-stu-id="d4143-166">**To set the relay state parameter**:</span></span>

1. <span data-ttu-id="d4143-167">Habilite a caixa de seleção **Mostrar configurações avançadas de URL** sob o título **Domínio e URLs** na folha de configuração do logon único.</span><span class="sxs-lookup"><span data-stu-id="d4143-167">Enable the **Show advanced URL settings** check-box under the **Domain and URLs** heading on the single-sign on configuration blade.</span></span> 
2. <span data-ttu-id="d4143-168">Depois de fazer isso, você verá um conjunto de novas caixas de entrada de URL que permitirá a definição dessas e de outras configurações de URL de SAML.</span><span class="sxs-lookup"><span data-stu-id="d4143-168">Once you do this, you’ll see a set of new URL input boxes appear which will allow you to set this, and other, SAML URL settings.</span></span>

## <a name="bring-your-own-password-sso-applications"></a><span data-ttu-id="d4143-169">Aplicativos SSO BYOP</span><span class="sxs-lookup"><span data-stu-id="d4143-169">Bring your own password SSO applications</span></span>

<span data-ttu-id="d4143-170">Sabemos que nem todos os aplicativos dão suporte à federação nativamente.</span><span class="sxs-lookup"><span data-stu-id="d4143-170">We know that not every application supports federation right out of the box.</span></span> <span data-ttu-id="d4143-171">Por exemplo, talvez um dos novos aplicativos que você adicionou tenha uma tela de logon personalizada em que os usuários usam um nome de usuário e uma senha para entrar.</span><span class="sxs-lookup"><span data-stu-id="d4143-171">For example, maybe one of the new applications you added has a custom login screen that your users use a username and password to sign in to.</span></span> <span data-ttu-id="d4143-172">Você ainda pode integrar esses tipos de aplicativos ao Azure AD usando nosso recurso **BYOA**, que agora está disponível para a configuração no novo portal.</span><span class="sxs-lookup"><span data-stu-id="d4143-172">You can still integrate these types of applications with Azure AD using our **Bring your own applications** feature, which is now available for you to configure in the new portal.</span></span>
 
  ![Integração de aplicativos de cofre de senha personalizados ao Azure AD](./media/active-directory-enterprise-apps-whats-new-azure-portal/13.png)

<span data-ttu-id="d4143-174">**Para conferir o recurso ‘BYOA’**:</span><span class="sxs-lookup"><span data-stu-id="d4143-174">**To check out the 'Bring your own applications' feature**:</span></span>

1. <span data-ttu-id="d4143-175">Depois de definir o modo de logon único para um novo aplicativo personalizado que você adicionou ao **Logon Único Baseado em Senha**, digite a URL onde o aplicativo processa sua tela de logon e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d4143-175">After you set the single sign-on mode for a new custom application that you’ve added to **Password-based Sign-on**, enter the URL where the application renders its login screen and click **Save**.</span></span>  
2. <span data-ttu-id="d4143-176">Depois de fazer isso, vamos extrair automaticamente essa URL para uma caixa de entrada de nome de usuário e de senha e permitir que você use o Azure AD para transmitir com segurança as senhas para o aplicativo usando a extensão de navegador de painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="d4143-176">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="configure-self-service-application-access"></a><span data-ttu-id="d4143-177">Configurar o acesso ao aplicativo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="d4143-177">Configure self-service application access</span></span>

<span data-ttu-id="d4143-178">Depois de adicionar muitos aplicativos novos, talvez você queira permitir que os usuários procurem e adicionem os aplicativos a seus próprios painéis de acesso, sem que seja necessária a intervenção de um administrador.</span><span class="sxs-lookup"><span data-stu-id="d4143-178">After you’ve added lots of new applications, maybe you want to allow your users to browse and add those applications to their own access panels, without needing to bother you as an administrator.</span></span> <span data-ttu-id="d4143-179">Com essa versão mais recente, você pode configurar e gerenciar o acesso a aplicativos de autoatendimento desde o novo portal.</span><span class="sxs-lookup"><span data-stu-id="d4143-179">Now, with this latest release, you can configure and manage self-service application access right from the new portal.</span></span>

  ![Configurar acesso ao aplicativo de autoatendimento para um aplicativo do SSO de senha](./media/active-directory-enterprise-apps-whats-new-azure-portal/14.png)
 
<span data-ttu-id="d4143-181">**Para configurar e gerenciar o acesso do aplicativo de autoatendimento**:</span><span class="sxs-lookup"><span data-stu-id="d4143-181">**To configure and manage self-service application access**:</span></span>

1. <span data-ttu-id="d4143-182">Para começar, você pode selecionar a opção **Autoatendimento** no menu de navegação à esquerda do aplicativo e definir a opção **Permitir que os usuários solicitem acesso a este aplicativo?** como '**Sim**'.</span><span class="sxs-lookup"><span data-stu-id="d4143-182">To get started, you can select the **Self-service** option from the application’s left navigation menu and set the **Allow users to request access to this application?** option to ‘**Yes**’.</span></span> 
2. <span data-ttu-id="d4143-183">Isso permitirá que você configure quem tem permissão para aprovar o acesso ao aplicativo e quais usuários de autoatendimento de grupo serão adicionados.</span><span class="sxs-lookup"><span data-stu-id="d4143-183">This will enable you to configure who is allowed to approve access to this application, and which group self-service users will be added.</span></span> <span data-ttu-id="d4143-184">Além disso, se o aplicativo estiver configurado para a senha de logon único, você também verá outra opção para permitir que os aprovadores gerenciem as senhas atribuídas ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4143-184">In addition, if the application is configured for password single-sign on, you’ll also see another option which lets you optionally allow those approvers to manage the passwords assigned to the application.</span></span>

##<a name="feedback"></a><span data-ttu-id="d4143-185">Comentários</span><span class="sxs-lookup"><span data-stu-id="d4143-185">Feedback</span></span>

<span data-ttu-id="d4143-186">Esperamos que você goste de usar a experiência aprimorada do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4143-186">We hope you like using the improved Azure AD experience.</span></span> <span data-ttu-id="d4143-187">Continue a fazer seus comentários!</span><span class="sxs-lookup"><span data-stu-id="d4143-187">Please keep the feedback coming!</span></span> <span data-ttu-id="d4143-188">Poste seus comentários e suas ideias para aprimoramento na seção **Portal de Administração** do nosso [fórum de comentários](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span><span class="sxs-lookup"><span data-stu-id="d4143-188">Post your feedback and ideas for improvement in the **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="d4143-189">Nós estamos empolgados para criar algo novo e interessante diariamente e usar suas diretrizes para formar e definir o que devemos criar a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4143-189">We’re excited about building cool new stuff every day, and use your guidance to shape and define what we build next.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4143-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4143-190">Next steps</span></span>

<span data-ttu-id="d4143-191">Para obter mais detalhes, confira [Gerenciamento de aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md).</span><span class="sxs-lookup"><span data-stu-id="d4143-191">For more details, see [Managing Applications with Azure Active Directory](active-directory-enable-sso-scenario.md).</span></span>



