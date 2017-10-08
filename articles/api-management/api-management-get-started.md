---
title: aaaManage sua primeira API no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como toocreate APIs, operações de adicionar e introdução ao gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="e75ae-103">Gerenciar sua primeira API no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="e75ae-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="e75ae-104"><a name="overview"> </a>Visão geral</span><span class="sxs-lookup"><span data-stu-id="e75ae-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="e75ae-105">Este guia mostra como tooquickly começar a usar o gerenciamento de API do Azure e fazer sua primeira chamada de API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="e75ae-106"><a name="concepts"> </a>O que é o Gerenciamento de API do Azure?</span><span class="sxs-lookup"><span data-stu-id="e75ae-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="e75ae-107">Você pode usar o gerenciamento de API do Azure tootake qualquer back-end e iniciar um programa de API totalmente desenvolvido com base nele.</span><span class="sxs-lookup"><span data-stu-id="e75ae-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="e75ae-108">Cenários comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="e75ae-108">Common scenarios include:</span></span>

* <span data-ttu-id="e75ae-109">**Proteção de infraestrutura móvel** com a retenção de acesso às chaves de API, impedindo ataques DOS ao usar limitação ou políticas avançadas de segurança como validação de token JWT.</span><span class="sxs-lookup"><span data-stu-id="e75ae-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="e75ae-110">**Habilitando ecossistemas de parceiro ISV** , oferecendo a integração de parceiro rápida por meio de desenvolvedor Olá portal e criação de um toodecouple de fachada de API de implementações internas que não são pronta para consumo do parceiro.</span><span class="sxs-lookup"><span data-stu-id="e75ae-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="e75ae-111">**Executando um programa de API interno** , oferecendo um local centralizado para Olá organização toocommunicate sobre a disponibilidade de saudação e mais recentes alterações tooAPIs, retenção de acesso com base em contas organizacionais, todas baseadas em um canal protegido entre Olá gateway de API e Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="e75ae-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="e75ae-112">sistema de saudação é composto de saudação componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="e75ae-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="e75ae-113">Olá **gateway API** é o ponto de extremidade de saudação que:</span><span class="sxs-lookup"><span data-stu-id="e75ae-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="e75ae-114">Aceita chamadas de API e roteia tooyour back-ends.</span><span class="sxs-lookup"><span data-stu-id="e75ae-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="e75ae-115">Verifica chaves de API, tokens JWT, certificados e outras credenciais.</span><span class="sxs-lookup"><span data-stu-id="e75ae-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="e75ae-116">Impõe o uso de cotas e limites de taxa.</span><span class="sxs-lookup"><span data-stu-id="e75ae-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="e75ae-117">Transforma sua API Olá imediatamente sem modificações no código.</span><span class="sxs-lookup"><span data-stu-id="e75ae-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="e75ae-118">Armazena respostas de back-end em cache em que a instalação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="e75ae-119">Registra logs de metadados de chamadas para fins de análise.</span><span class="sxs-lookup"><span data-stu-id="e75ae-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="e75ae-120">Olá **portal do publicador** é a interface administrativa hello, em que você configurar o programa de API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="e75ae-121">Use-o para:</span><span class="sxs-lookup"><span data-stu-id="e75ae-121">Use it to:</span></span>
  
  * <span data-ttu-id="e75ae-122">Definir ou importar esquema de API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-122">Define or import API schema.</span></span>
  * <span data-ttu-id="e75ae-123">Empacotar APIs em produtos.</span><span class="sxs-lookup"><span data-stu-id="e75ae-123">Package APIs into products.</span></span>
  * <span data-ttu-id="e75ae-124">Configure políticas, como cotas ou transformações em Olá APIs.</span><span class="sxs-lookup"><span data-stu-id="e75ae-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="e75ae-125">Obter insights por meio de análises.</span><span class="sxs-lookup"><span data-stu-id="e75ae-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="e75ae-126">Gerenciar usuários.</span><span class="sxs-lookup"><span data-stu-id="e75ae-126">Manage users.</span></span>
* <span data-ttu-id="e75ae-127">Olá **portal do desenvolvedor** serve como a presença do Olá web principal para desenvolvedores, onde eles podem:</span><span class="sxs-lookup"><span data-stu-id="e75ae-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="e75ae-128">Ler a documentação da API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-128">Read API documentation.</span></span>
  * <span data-ttu-id="e75ae-129">Experimente uma API via console interativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="e75ae-130">Criar uma conta e assinar chaves tooget API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="e75ae-131">Acessar a análise do seu próprio uso.</span><span class="sxs-lookup"><span data-stu-id="e75ae-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="e75ae-132"><a name="create-service-instance"> </a>Criar uma instância de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="e75ae-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="e75ae-133">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e75ae-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="e75ae-134">Se você não tem uma conta, pode criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e75ae-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="e75ae-135">Para obter detalhes, consulte [Avaliação gratuita do Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="e75ae-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="e75ae-136">Olá primeira etapa ao trabalhar com gerenciamento de API é toocreate uma instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="e75ae-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="e75ae-137">Entrar toohello [Portal do Azure] [ Azure Portal] e clique em **novo**, **Web + móvel**, **gerenciamento de API**.</span><span class="sxs-lookup"><span data-stu-id="e75ae-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Nova instância do Gerenciamento de API][api-management-create-instance-menu]

<span data-ttu-id="e75ae-139">Para **nome**, especifique um toouse de nome de subdomínio exclusivo para a URL do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="e75ae-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="e75ae-140">Escolha a saudação desejada **assinatura**, **grupo de recursos** e **local** para sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="e75ae-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="e75ae-141">Digite **Contoso Ltd.** para Olá **nome da organização**e insira seu endereço de email no hello **email do administrador** campo.</span><span class="sxs-lookup"><span data-stu-id="e75ae-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="e75ae-142">Este endereço de email é usado para notificações do sistema de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="e75ae-143">Para obter mais informações, consulte [como tooconfigure notificações e modelos no gerenciamento de API do Azure de email][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e75ae-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Novo serviço de Gerenciamento de API][api-management-create-instance-step1]

<span data-ttu-id="e75ae-145">As instâncias de serviço de Gerenciamento de API estão disponíveis em três camadas: Developer, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="e75ae-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="e75ae-146">Saudação da camada de desenvolvedor é para o desenvolvimento, testes e programas piloto de API em que a alta disponibilidade não é uma preocupação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="e75ae-147">Saudação padrão e as camadas Premium, você pode dimensionar seu toohandle de contagem de unidade reservada mais tráfego.</span><span class="sxs-lookup"><span data-stu-id="e75ae-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="e75ae-148">as camadas Standard e Premium Olá fornecem o serviço de gerenciamento de API com hello mais potência de processamento e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="e75ae-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="e75ae-149">Você pode concluir este tutorial usando qualquer camada.</span><span class="sxs-lookup"><span data-stu-id="e75ae-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="e75ae-150">Para obter mais informações sobre as camadas de Gerenciamento de API, confira [Preços de Gerenciamento de API][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="e75ae-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="e75ae-151">Clique em **criar** toostart sua instância de serviço de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="e75ae-151">Click **Create** toostart provisioning your service instance.</span></span>

![Novo serviço de Gerenciamento de API][api-management-instance-created]

<span data-ttu-id="e75ae-153">Depois de criar a instância do serviço hello, próxima etapa de saudação é toocreate ou importar uma API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="e75ae-154"><a name="create-api"> </a>Importar uma API</span><span class="sxs-lookup"><span data-stu-id="e75ae-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="e75ae-155">Uma API consiste em um conjunto de operações que podem ser iniciadas a partir de uma aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="e75ae-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="e75ae-156">Operações de API são serviços da web de tooexisting por proxy.</span><span class="sxs-lookup"><span data-stu-id="e75ae-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="e75ae-157">APIs podem ser criadas (e as operações podem ser adicionadas) manualmente, podendo também ser importadas.</span><span class="sxs-lookup"><span data-stu-id="e75ae-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="e75ae-158">Neste tutorial, vamos importar hello API para um serviço da web exemplo Calculadora fornecidos pela Microsoft e hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="e75ae-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e75ae-159">Para obter orientação sobre como criar uma API e operações de adicionar manualmente, consulte [como toocreate APIs](api-management-howto-create-apis.md) e [como tooadd operações tooan API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="e75ae-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="e75ae-160">APIs são configuradas no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="e75ae-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="e75ae-161">tooreach-la, clique em **portal do publicador** na barra de ferramentas de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="e75ae-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="e75ae-163">Calculadora de saudação tooimport API, clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **importação API**.</span><span class="sxs-lookup"><span data-stu-id="e75ae-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Botão Importar API][api-management-import-api]

<span data-ttu-id="e75ae-165">Execute Olá etapas tooconfigure Olá Calculadora API a seguir:</span><span class="sxs-lookup"><span data-stu-id="e75ae-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="e75ae-166">Clique em **From URL**, digite **http://calcapi.cloudapp.net/calcapi.json** em Olá **URL do documento de especificação** texto caixa e, em seguida, clique em Olá **Swagger**  botão de opção.</span><span class="sxs-lookup"><span data-stu-id="e75ae-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="e75ae-167">Tipo **calc** em Olá **sufixo de URL da API da Web** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e75ae-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="e75ae-168">Clique em Olá **produtos (opcionais)** caixa e escolha **Starter**.</span><span class="sxs-lookup"><span data-stu-id="e75ae-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="e75ae-169">Clique em **salvar** tooimport Olá API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-169">Click **Save** tooimport hello API.</span></span>

![Adicionar nova API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="e75ae-171">**Gerenciamento de API** atualmente oferece suporte à versão 1.2 e 2.0 do documento de Swagger para importação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="e75ae-172">Certifique-se de que, mesmo que a [Especificação Swagger 2.0](http://swagger.io/specification) declare que as propriedades `host`, `basePath` e `schemes` são opcionais, o documento de Swagger 2.0 **PRECISA** conter essas propriedades; caso contrário, não será importado.</span><span class="sxs-lookup"><span data-stu-id="e75ae-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="e75ae-173">Depois que Olá API é importado, hello página Resumo para a API de saudação é exibida no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="e75ae-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Resumo da API][api-management-imported-api-summary]

<span data-ttu-id="e75ae-175">Olá seção API tem várias guias.</span><span class="sxs-lookup"><span data-stu-id="e75ae-175">hello API section has several tabs.</span></span> <span data-ttu-id="e75ae-176">Olá **resumo** guia exibe informações sobre a API de saudação e métricas básicas.</span><span class="sxs-lookup"><span data-stu-id="e75ae-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="e75ae-177">Olá [configurações](api-management-howto-create-apis.md#configure-api-settings) guia é usada configuração de Olá tooview e edição de uma API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="e75ae-178">Olá [operações](api-management-howto-add-operations.md) guia é operações toomanage usado Olá da API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="e75ae-179">Olá **segurança** guia pode ser usado tooconfigure autenticação de gateway para o servidor de back-end de saudação usando autenticação básica ou [autenticação mútua de certificado](api-management-howto-mutual-certificates.md)e tooconfigure [ autorização do usuário usando o OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="e75ae-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="e75ae-180">Olá **problemas** guia é tooview usado problemas relatados por desenvolvedores de saudação que estão usando suas APIs.</span><span class="sxs-lookup"><span data-stu-id="e75ae-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="e75ae-181">Olá **produtos** guia é usada tooconfigure produtos de Olá que contêm essa API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="e75ae-182">Por padrão, cada instância de Gerenciamento de API é fornecida com dois produtos função Web:</span><span class="sxs-lookup"><span data-stu-id="e75ae-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="e75ae-183">**Inicial**</span><span class="sxs-lookup"><span data-stu-id="e75ae-183">**Starter**</span></span>
* <span data-ttu-id="e75ae-184">**Ilimitado**</span><span class="sxs-lookup"><span data-stu-id="e75ae-184">**Unlimited**</span></span>

<span data-ttu-id="e75ae-185">Neste tutorial, Olá API de calculadora básica foi adicionado produto de iniciador toohello quando Olá API foi importado.</span><span class="sxs-lookup"><span data-stu-id="e75ae-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="e75ae-186">Na ordem toomake chamadas tooan API, os desenvolvedores devem assinar primeiro produto tooa que lhes dá acesso tooit.</span><span class="sxs-lookup"><span data-stu-id="e75ae-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="e75ae-187">Os desenvolvedores podem assinar tooproducts no portal do desenvolvedor hello, ou os administradores podem assinar tooproducts de desenvolvedores no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="e75ae-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="e75ae-188">Você é um administrador, desde que você criou instância de gerenciamento de API de saudação em Olá etapas anteriores no tutorial Olá, portanto você já está inscrito tooevery produto por padrão.</span><span class="sxs-lookup"><span data-stu-id="e75ae-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="e75ae-189"><a name="call-operation"></a>Chamar uma operação do portal do desenvolvedor Olá</span><span class="sxs-lookup"><span data-stu-id="e75ae-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="e75ae-190">Operações podem ser chamadas diretamente no portal do desenvolvedor hello, que fornece uma maneira conveniente de tooview e testar as operações de saudação de uma API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="e75ae-191">Nesta etapa do tutorial, você chamará Olá básica Calculadora API **adicionar dois inteiros** operação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="e75ae-192">Clique em **portal do desenvolvedor** do menu de saudação à saudação parte superior direita do portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="e75ae-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="e75ae-194">Clique em **APIs** no menu superior hello e clique **Calculadora básica** toosee Olá operações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e75ae-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-calc-api]

<span data-ttu-id="e75ae-196">Observe as descrições do exemplo hello e parâmetros que foram importados juntamente com hello API e operações, fornecendo a documentação para desenvolvedores de saudação que usará esta operação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="e75ae-197">Essas descrições também podem ser adicionadas quando as operações são adicionadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="e75ae-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="e75ae-198">Olá toocall **adicionar dois inteiros** operação, clique em **Experimente**.</span><span class="sxs-lookup"><span data-stu-id="e75ae-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Experimente][api-management-developer-portal-calc-api-console]

<span data-ttu-id="e75ae-200">Insira alguns valores para parâmetros de saudação ou manter Olá padrões e, em seguida, clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="e75ae-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="e75ae-202">Depois que uma operação é invocada, portal do desenvolvedor Olá exibe Olá **status da resposta**, Olá **cabeçalhos de resposta**e qualquer **conteúdo de resposta**.</span><span class="sxs-lookup"><span data-stu-id="e75ae-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Resposta][api-management-invoke-get-response]

## <span data-ttu-id="e75ae-204"><a name="view-analytics"> </a>Exibir análise</span><span class="sxs-lookup"><span data-stu-id="e75ae-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="e75ae-205">análise tooview para Calculadora básica, portal do publicador switch back toohello selecionando **gerenciar** do menu de saudação à saudação parte superior direita do portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="e75ae-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Gerenciar][api-management-manage-menu]

<span data-ttu-id="e75ae-207">modo de exibição padrão para o portal do publicador Olá Olá é hello **painel**, que fornece uma visão geral de sua instância de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Painel][api-management-dashboard]

<span data-ttu-id="e75ae-209">Passe o mouse sobre o gráfico para Olá Olá **Calculadora básica** métricas específicas do hello toosee de uso de saudação do hello API para um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="e75ae-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="e75ae-210">Se você não vir todas as linhas do gráfico, alterne o portal do desenvolvedor toohello voltar e fazer algumas chamadas na API de saudação, aguarde alguns instantes e vêm toohello painel.</span><span class="sxs-lookup"><span data-stu-id="e75ae-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="e75ae-211">Clique em **exibir detalhes** tooview Olá página de resumo Olá API, incluindo uma versão maior de métricas de saudação exibida.</span><span class="sxs-lookup"><span data-stu-id="e75ae-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Análise][api-management-mouse-over]

![Resumo][api-management-api-summary-metrics]

<span data-ttu-id="e75ae-214">Para métricas detalhadas e relatórios, clique em **análise** de saudação **gerenciamento de API** menu Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="e75ae-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Visão geral][api-management-analytics-overview]

<span data-ttu-id="e75ae-216">Olá **análise** seção tem Olá quatro guias a seguir:</span><span class="sxs-lookup"><span data-stu-id="e75ae-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="e75ae-217">**Em um relance** fornece o uso geral e métricas de integridade, bem como Olá melhores desenvolvedores, principais produtos, principais APIs e operações principais.</span><span class="sxs-lookup"><span data-stu-id="e75ae-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="e75ae-218">**Uso** fornece uma visão mais detalhada das chamadas à API e da largura de banda, incluindo uma representação geográfica.</span><span class="sxs-lookup"><span data-stu-id="e75ae-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="e75ae-219">**Integridade** abrange os códigos de status, taxas de êxito do cache, tempos de resposta e tempos de resposta de serviço e da API.</span><span class="sxs-lookup"><span data-stu-id="e75ae-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="e75ae-220">**Atividade** fornece relatórios que fazem busca detalhada sobre a atividade específica Olá pelo desenvolvedor, produto, API e operação.</span><span class="sxs-lookup"><span data-stu-id="e75ae-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="e75ae-221"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e75ae-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="e75ae-222">Saiba como muito[proteger sua API com os limites de taxa](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e75ae-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
