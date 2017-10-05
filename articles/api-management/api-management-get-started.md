---
title: Gerenciar sua primeira API no Gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como criar APIs, adicionar operações e obtenha uma introdução ao Gerenciamento de API."
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
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="d451b-103">Gerenciar sua primeira API no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="d451b-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="d451b-104"><a name="overview"> </a>Visão geral</span><span class="sxs-lookup"><span data-stu-id="d451b-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="d451b-105">Este guia mostra como começar rapidamente a usar o Gerenciamento de API do Azure e como fazer sua primeira chamada à API.</span><span class="sxs-lookup"><span data-stu-id="d451b-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="d451b-106"><a name="concepts"> </a>O que é o Gerenciamento de API do Azure?</span><span class="sxs-lookup"><span data-stu-id="d451b-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="d451b-107">O Gerenciamento de API do Azure permite usar qualquer back-end e lançar um programa completo de API com base nele.</span><span class="sxs-lookup"><span data-stu-id="d451b-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="d451b-108">Cenários comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="d451b-108">Common scenarios include:</span></span>

* <span data-ttu-id="d451b-109">**Proteção de infraestrutura móvel** com a retenção de acesso às chaves de API, impedindo ataques DOS ao usar limitação ou políticas avançadas de segurança como validação de token JWT.</span><span class="sxs-lookup"><span data-stu-id="d451b-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="d451b-110">**Habilitação de ecossistemas de parceiro ISV** oferecendo integração rápida de parceiro através do portal do desenvolvedor e criando uma fachada de API para desassociação de implementações internas não prontas para consumo de parceiro.</span><span class="sxs-lookup"><span data-stu-id="d451b-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="d451b-111">**Execução de um programa de API interno** oferecendo um local centralizado para a organização se comunicar sobre a disponibilidade e as alterações mais recentes de APIs, retenção de acesso com base em contas organizacionais, tudo baseado em um canal protegido entre o gateway de API e o back-end.</span><span class="sxs-lookup"><span data-stu-id="d451b-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="d451b-112">O sistema é composto pelos seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="d451b-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="d451b-113">O **gateway de API** é o ponto de extremidade que:</span><span class="sxs-lookup"><span data-stu-id="d451b-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="d451b-114">Aceita chamadas de API e as direciona para seu back-ends.</span><span class="sxs-lookup"><span data-stu-id="d451b-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="d451b-115">Verifica chaves de API, tokens JWT, certificados e outras credenciais.</span><span class="sxs-lookup"><span data-stu-id="d451b-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="d451b-116">Impõe o uso de cotas e limites de taxa.</span><span class="sxs-lookup"><span data-stu-id="d451b-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="d451b-117">Transforma sua API imediatamente sem modificações no código.</span><span class="sxs-lookup"><span data-stu-id="d451b-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="d451b-118">Armazena respostas de back-end em cache em que a instalação.</span><span class="sxs-lookup"><span data-stu-id="d451b-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="d451b-119">Registra logs de metadados de chamadas para fins de análise.</span><span class="sxs-lookup"><span data-stu-id="d451b-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="d451b-120">O **portal do editor** é a interface administrativa na qual você configura seu programa de API.</span><span class="sxs-lookup"><span data-stu-id="d451b-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="d451b-121">Use-o para:</span><span class="sxs-lookup"><span data-stu-id="d451b-121">Use it to:</span></span>
  
  * <span data-ttu-id="d451b-122">Definir ou importar esquema de API.</span><span class="sxs-lookup"><span data-stu-id="d451b-122">Define or import API schema.</span></span>
  * <span data-ttu-id="d451b-123">Empacotar APIs em produtos.</span><span class="sxs-lookup"><span data-stu-id="d451b-123">Package APIs into products.</span></span>
  * <span data-ttu-id="d451b-124">Políticas de configuração como cotas ou transformações em APIs.</span><span class="sxs-lookup"><span data-stu-id="d451b-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="d451b-125">Obter insights por meio de análises.</span><span class="sxs-lookup"><span data-stu-id="d451b-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="d451b-126">Gerenciar usuários.</span><span class="sxs-lookup"><span data-stu-id="d451b-126">Manage users.</span></span>
* <span data-ttu-id="d451b-127">O **portal do desenvolvedor** serve como a presença da web principal para desenvolvedores, na qual eles podem:</span><span class="sxs-lookup"><span data-stu-id="d451b-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="d451b-128">Ler a documentação da API.</span><span class="sxs-lookup"><span data-stu-id="d451b-128">Read API documentation.</span></span>
  * <span data-ttu-id="d451b-129">Experimentar uma API por meio do console interativo.</span><span class="sxs-lookup"><span data-stu-id="d451b-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="d451b-130">Criar uma conta e fazer uma assinatura para obter chaves de API.</span><span class="sxs-lookup"><span data-stu-id="d451b-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="d451b-131">Acessar a análise do seu próprio uso.</span><span class="sxs-lookup"><span data-stu-id="d451b-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="d451b-132"><a name="create-service-instance"> </a>Criar uma instância de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="d451b-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="d451b-133">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d451b-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d451b-134">Se você não tem uma conta, pode criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d451b-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="d451b-135">Para obter detalhes, consulte [Avaliação gratuita do Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="d451b-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="d451b-136">Esta etapa sobre como trabalhar com o Gerenciamento de API serve para criar uma instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="d451b-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="d451b-137">Entre no [Portal do Azure][Azure Portal] e clique em **Novo**, **Web + Móvel** e **Gerenciamento de API**.</span><span class="sxs-lookup"><span data-stu-id="d451b-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Nova instância do Gerenciamento de API][api-management-create-instance-menu]

<span data-ttu-id="d451b-139">Para **Nome**, especifique um nome de subdomínio exclusivo para usar na URL do serviço.</span><span class="sxs-lookup"><span data-stu-id="d451b-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="d451b-140">Selecione a **Assinatura**, **Grupo de recursos** e **Local** desejados para sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="d451b-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="d451b-141">Digite **Contoso Ltd.**</span><span class="sxs-lookup"><span data-stu-id="d451b-141">Enter **Contoso Ltd.**</span></span> <span data-ttu-id="d451b-142">como o **Nome da Organização** e insira seu endereço de email no campo de **Email do Administrador**.</span><span class="sxs-lookup"><span data-stu-id="d451b-142">for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="d451b-143">Esse endereço de email é usado para notificações do sistema de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="d451b-143">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="d451b-144">Para obter mais informações, confira [Saiba como configurar notificações e modelos de email no Gerenciamento de API do Azure][How to configure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="d451b-144">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Novo serviço de Gerenciamento de API][api-management-create-instance-step1]

<span data-ttu-id="d451b-146">As instâncias de serviço de Gerenciamento de API estão disponíveis em três camadas: Developer, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="d451b-146">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="d451b-147">A Camada do Desenvolvedor é para programas pilotos de API, teste e desenvolvimento, onde a alta disponibilidade não é uma preocupação.</span><span class="sxs-lookup"><span data-stu-id="d451b-147">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="d451b-148">Nas camadas Standard e Premium, você pode dimensionar sua contagem de unidade reservada para lidar com mais tráfego.</span><span class="sxs-lookup"><span data-stu-id="d451b-148">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="d451b-149">As camadas Standard e Premium fornecem um serviço de Gerenciamento de API com o maior poder de processamento e desempenho.</span><span class="sxs-lookup"><span data-stu-id="d451b-149">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="d451b-150">Você pode concluir este tutorial usando qualquer camada.</span><span class="sxs-lookup"><span data-stu-id="d451b-150">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="d451b-151">Para obter mais informações sobre as camadas de Gerenciamento de API, confira [Preços de Gerenciamento de API][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="d451b-151">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="d451b-152">Clique em **Criar** para iniciar a instância do serviço de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d451b-152">Click **Create** to start provisioning your service instance.</span></span>

![Novo serviço de Gerenciamento de API][api-management-instance-created]

<span data-ttu-id="d451b-154">Após criar a instância de serviço, a próxima etapa é criar ou importar a API.</span><span class="sxs-lookup"><span data-stu-id="d451b-154">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="d451b-155"><a name="create-api"> </a>Importar uma API</span><span class="sxs-lookup"><span data-stu-id="d451b-155"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="d451b-156">Uma API consiste em um conjunto de operações que podem ser iniciadas a partir de uma aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="d451b-156">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="d451b-157">Todas as operações de API são colocadas em proxies de serviços Web existentes.</span><span class="sxs-lookup"><span data-stu-id="d451b-157">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="d451b-158">APIs podem ser criadas (e as operações podem ser adicionadas) manualmente, podendo também ser importadas.</span><span class="sxs-lookup"><span data-stu-id="d451b-158">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="d451b-159">Neste tutorial, importaremos uma API para um serviço Web de calculadora de exemplo fornecida pela Microsoft e hospedada no Azure.</span><span class="sxs-lookup"><span data-stu-id="d451b-159">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d451b-160">Para obter diretrizes sobre como criar uma API e adicionar operações manualmente, consulte [Como criar APIs](api-management-howto-create-apis.md) e [Como adicionar operações a uma API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d451b-160">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="d451b-161">APIs são configuradas no Portal do editor.</span><span class="sxs-lookup"><span data-stu-id="d451b-161">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="d451b-162">Para alcançá-lo, clique em **Portal do editor** na barra de ferramentas do serviço.</span><span class="sxs-lookup"><span data-stu-id="d451b-162">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="d451b-164">Para importar a API de calculadora, clique em **APIs** no menu **Gerenciamento de API** à esquerda e depois clique em **Importar API**.</span><span class="sxs-lookup"><span data-stu-id="d451b-164">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Botão Importar API][api-management-import-api]

<span data-ttu-id="d451b-166">Execute as seguintes etapas para configurar a API de calculadora:</span><span class="sxs-lookup"><span data-stu-id="d451b-166">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="d451b-167">Clique em **Da URL**, digite **http://calcapi.cloudapp.net/calcapi.json** na caixa de texto **URL do documento de especificação** e clique no botão de opção **Swagger**.</span><span class="sxs-lookup"><span data-stu-id="d451b-167">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="d451b-168">Digite **calc** na caixa de texto **Sufixo da URL da API Web**.</span><span class="sxs-lookup"><span data-stu-id="d451b-168">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="d451b-169">Clique na caixa **Produtos (opcional)** e escolha **Inicial**.</span><span class="sxs-lookup"><span data-stu-id="d451b-169">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="d451b-170">Clique em **Salvar** para importar a API.</span><span class="sxs-lookup"><span data-stu-id="d451b-170">Click **Save** to import the API.</span></span>

![Adicionar nova API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="d451b-172">**Gerenciamento de API** atualmente oferece suporte à versão 1.2 e 2.0 do documento de Swagger para importação.</span><span class="sxs-lookup"><span data-stu-id="d451b-172">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="d451b-173">Certifique-se de que, mesmo que a [Especificação Swagger 2.0](http://swagger.io/specification) declare que as propriedades `host`, `basePath` e `schemes` são opcionais, o documento de Swagger 2.0 **PRECISA** conter essas propriedades; caso contrário, não será importado.</span><span class="sxs-lookup"><span data-stu-id="d451b-173">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="d451b-174">Depois que a API é importada, a página de resumo para a API é exibida no portal do editor.</span><span class="sxs-lookup"><span data-stu-id="d451b-174">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![Resumo da API][api-management-imported-api-summary]

<span data-ttu-id="d451b-176">A seção API tem várias guias.</span><span class="sxs-lookup"><span data-stu-id="d451b-176">The API section has several tabs.</span></span> <span data-ttu-id="d451b-177">A guia **Resumo** exibe as métricas básicas e as informações sobre a API.</span><span class="sxs-lookup"><span data-stu-id="d451b-177">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="d451b-178">A guia [Configurações](api-management-howto-create-apis.md#configure-api-settings) é usada para exibir e editar a configuração de uma API.</span><span class="sxs-lookup"><span data-stu-id="d451b-178">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="d451b-179">A guia [Operações](api-management-howto-add-operations.md) é usada para gerenciar as operações da API.</span><span class="sxs-lookup"><span data-stu-id="d451b-179">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="d451b-180">A guia **Segurança** pode ser usada para configurar a autenticação de gateway para o servidor de back-end usando a autenticação Básica ou [autenticação mútua de certificados](api-management-howto-mutual-certificates.md), bem como para configurar a [autorização do usuário usando OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="d451b-180">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="d451b-181">A guia **Problemas** é usada para exibir os problemas relatados pelos desenvolvedores que utilizam suas APIs.</span><span class="sxs-lookup"><span data-stu-id="d451b-181">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="d451b-182">A guia **Produtos** é usada para configurar os produtos que contêm essa API.</span><span class="sxs-lookup"><span data-stu-id="d451b-182">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="d451b-183">Por padrão, cada instância de Gerenciamento de API é fornecida com dois produtos função Web:</span><span class="sxs-lookup"><span data-stu-id="d451b-183">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="d451b-184">**Inicial**</span><span class="sxs-lookup"><span data-stu-id="d451b-184">**Starter**</span></span>
* <span data-ttu-id="d451b-185">**Ilimitado**</span><span class="sxs-lookup"><span data-stu-id="d451b-185">**Unlimited**</span></span>

<span data-ttu-id="d451b-186">Neste tutorial, a API Calculadora Básica foi adicionada ao produto Inicial quando a API foi importada.</span><span class="sxs-lookup"><span data-stu-id="d451b-186">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="d451b-187">Para fazer chamadas para uma API, os desenvolvedores precisam primeiro assinar um produto que concede acesso a ela.</span><span class="sxs-lookup"><span data-stu-id="d451b-187">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="d451b-188">Os desenvolvedores podem assinar os produtos no Portal do Desenvolvedor ou os administradores podem inscrever os desenvolvedores nos produtos no portal do editor.</span><span class="sxs-lookup"><span data-stu-id="d451b-188">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="d451b-189">Você é o administrador porque criou a instância de Gerenciamento de API nas etapas anteriores do tutorial, por isso já se inscreveu em todos os produtos por padrão.</span><span class="sxs-lookup"><span data-stu-id="d451b-189">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="d451b-190"><a name="call-operation"> </a>Chamar uma operação no portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="d451b-190"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="d451b-191">As operações podem ser chamadas diretamente do portal do desenvolvedor, que fornece uma forma conveniente de exibir e testar as operações de uma API.</span><span class="sxs-lookup"><span data-stu-id="d451b-191">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="d451b-192">Nesta etapa do tutorial, você chamará a operação **Adicionar dois inteiros** da API da Calculadora Básica.</span><span class="sxs-lookup"><span data-stu-id="d451b-192">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="d451b-193">Clique em **Portal do Desenvolvedor** no menu da parte superior direita do portal do editor.</span><span class="sxs-lookup"><span data-stu-id="d451b-193">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="d451b-195">Clique em **APIs** no menu superior e depois clique em **Calculadora Básica** para ver as operações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d451b-195">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-calc-api]

<span data-ttu-id="d451b-197">Observe as descrições e parâmetros de exemplo que foram importados juntamente com a API e operações, fornecendo documentação para os desenvolvedores que usarão esta operação.</span><span class="sxs-lookup"><span data-stu-id="d451b-197">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="d451b-198">Essas descrições também podem ser adicionadas quando as operações são adicionadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="d451b-198">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="d451b-199">Para chamar a operação **Adicionar dois inteiros**, clique em **Experimente**.</span><span class="sxs-lookup"><span data-stu-id="d451b-199">To call the **Add two integers** operation, click **Try it**.</span></span>

![Experimente][api-management-developer-portal-calc-api-console]

<span data-ttu-id="d451b-201">Você pode inserir alguns valores para os parâmetros ou manter os padrões, depois clicar em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="d451b-201">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="d451b-203">Após invocar uma operação, o portal do desenvolvedor exibe o **Status de resposta**, os **Cabeçalhos de resposta** e o **Conteúdo de resposta**.</span><span class="sxs-lookup"><span data-stu-id="d451b-203">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Response][api-management-invoke-get-response]

## <span data-ttu-id="d451b-205"><a name="view-analytics"> </a>Exibir análise</span><span class="sxs-lookup"><span data-stu-id="d451b-205"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="d451b-206">Para exibir a análise da Calculadora Básica, alterne para o portal do editor selecionando **Gerenciar** no menu na parte superior direita do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="d451b-206">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![Gerenciar][api-management-manage-menu]

<span data-ttu-id="d451b-208">A exibição padrão do portal do editor é o **Painel**, que fornece uma visão geral da instância de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="d451b-208">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Painel][api-management-dashboard]

<span data-ttu-id="d451b-210">Passe o mouse sobre o gráfico da **Calculadora Básica** para ver as métricas específicas de utilização da API durante um período de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="d451b-210">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="d451b-211">Se você não vir linhas no gráfico, volte ao portal do desenvolvedor e faça algumas chamadas à API, aguarde alguns momentos e volte para o painel.</span><span class="sxs-lookup"><span data-stu-id="d451b-211">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="d451b-212">Clique em **Exibir detalhes** para exibir a página de resumo da API, incluindo uma versão maior das métricas exibidas.</span><span class="sxs-lookup"><span data-stu-id="d451b-212">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![Análise][api-management-mouse-over]

![Resumo][api-management-api-summary-metrics]

<span data-ttu-id="d451b-215">Para obter métricas e relatórios detalhados, clique em **Analytics** no menu **Gerenciamento de API** à esquerda.</span><span class="sxs-lookup"><span data-stu-id="d451b-215">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![Visão geral][api-management-analytics-overview]

<span data-ttu-id="d451b-217">A seção **Análise** possui as quatro guias a seguir.</span><span class="sxs-lookup"><span data-stu-id="d451b-217">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="d451b-218">**Em um relance** fornece a utilização e as métricas de integridade gerais, bem como desenvolvedores, APIs e operações principais.</span><span class="sxs-lookup"><span data-stu-id="d451b-218">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="d451b-219">**Uso** fornece uma visão mais detalhada das chamadas à API e da largura de banda, incluindo uma representação geográfica.</span><span class="sxs-lookup"><span data-stu-id="d451b-219">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="d451b-220">**Integridade** abrange os códigos de status, taxas de êxito do cache, tempos de resposta e tempos de resposta de serviço e da API.</span><span class="sxs-lookup"><span data-stu-id="d451b-220">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="d451b-221">**Atividade** fornece os relatórios que fazer o detalhamento até a atividade específica por desenvolvedor, produto, API e operação.</span><span class="sxs-lookup"><span data-stu-id="d451b-221">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="d451b-222"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d451b-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="d451b-223">Saiba como [Proteger sua API com limites de taxas](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="d451b-223">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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
