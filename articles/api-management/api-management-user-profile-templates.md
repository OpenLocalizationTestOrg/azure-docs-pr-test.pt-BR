---
title: "AAA \"modelos de perfil de usuário no gerenciamento de API do Azure | Microsoft Docs\""
description: "Saiba como páginas de conteúdo toocustomize Olá Olá perfil de usuário no portal do desenvolvedor Olá no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="8fd09-103">Modelos de perfil de usuário no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="8fd09-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="8fd09-104">Gerenciamento de API do Azure fornece que Olá conteúdo de saudação toocustomize capacidade de páginas de portal do desenvolvedor usando um conjunto de modelos que configurar seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8fd09-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="8fd09-105">Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e hello editor de sua escolha, como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto fornecido de localizadas [recursos de cadeia de caracteres](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controles](api-management-page-controls.md), você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar usar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="8fd09-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="8fd09-106">Olá modelos nesta seção permitem toocustomize conteúdo de saudação de páginas de perfil de usuário Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-106">hello templates in this section allow you toocustomize hello content of hello User profile pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="8fd09-107">Perfil</span><span class="sxs-lookup"><span data-stu-id="8fd09-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="8fd09-108">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="8fd09-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="8fd09-109">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="8fd09-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="8fd09-110">Atualizar informações da conta</span><span class="sxs-lookup"><span data-stu-id="8fd09-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="8fd09-111">Modelos de padrão de exemplo estão incluídos no hello documentação a seguir, mas são toochange assunto devido a melhorias toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="8fd09-111">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="8fd09-112">Você pode exibir modelos do saudação padrão em tempo real no portal do desenvolvedor Olá navegando modelos individuais toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="8fd09-112">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="8fd09-113">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="8fd09-113">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="8fd09-114"><a name="Profile"></a> Perfil</span><span class="sxs-lookup"><span data-stu-id="8fd09-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="8fd09-115">Olá **perfil** modelo permite que você toocustomize seção de perfil de usuário Olá da página de perfil de usuário Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-115">hello **profile** template allows you toocustomize hello user profile section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8fd09-116">![Página de perfil do usuário](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Página de perfil do usuário de APIM")</span><span class="sxs-lookup"><span data-stu-id="8fd09-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8fd09-117">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="8fd09-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="8fd09-118">Controles</span><span class="sxs-lookup"><span data-stu-id="8fd09-118">Controls</span></span>  
 <span data-ttu-id="8fd09-119">Este modelo pode não usar nenhum [controle de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="8fd09-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="8fd09-120">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="8fd09-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8fd09-121">Olá [perfil](#Profile), [aplicativos](#Applications), e [assinaturas](#Subscriptions) modelos compartilham Olá mesmo dados modelam e recebem Olá mesmos dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="8fd09-121">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="8fd09-122">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8fd09-122">Property</span></span>|<span data-ttu-id="8fd09-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="8fd09-123">Type</span></span>|<span data-ttu-id="8fd09-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="8fd09-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="8fd09-125">firstName</span><span class="sxs-lookup"><span data-stu-id="8fd09-125">firstName</span></span>|<span data-ttu-id="8fd09-126">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-126">string</span></span>|<span data-ttu-id="8fd09-127">Nome do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-127">First name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-128">lastName</span><span class="sxs-lookup"><span data-stu-id="8fd09-128">lastName</span></span>|<span data-ttu-id="8fd09-129">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-129">string</span></span>|<span data-ttu-id="8fd09-130">Sobrenome do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-130">Last name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-131">companyName</span><span class="sxs-lookup"><span data-stu-id="8fd09-131">companyName</span></span>|<span data-ttu-id="8fd09-132">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-132">string</span></span>|<span data-ttu-id="8fd09-133">nome da empresa do usuário atual Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="8fd09-133">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="8fd09-134">addresserEmail</span></span>|<span data-ttu-id="8fd09-135">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-135">string</span></span>|<span data-ttu-id="8fd09-136">Endereço de email do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-136">Email address of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="8fd09-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="8fd09-138">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-138">string</span></span>|<span data-ttu-id="8fd09-139">Análise de tooview de URL relativo para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-139">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="8fd09-140">subscriptions</span></span>|<span data-ttu-id="8fd09-141">Coleção de entidades de [Assinatura](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="8fd09-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="8fd09-142">assinaturas de saudação para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-142">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-143">de dimensionamento da Web</span><span class="sxs-lookup"><span data-stu-id="8fd09-143">applications</span></span>|<span data-ttu-id="8fd09-144">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="8fd09-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="8fd09-145">aplicativos de saudação do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-145">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="8fd09-146">changePasswordUrl</span></span>|<span data-ttu-id="8fd09-147">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-147">string</span></span>|<span data-ttu-id="8fd09-148">Olá relativo URL toochange Olá senha do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="8fd09-148">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="8fd09-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="8fd09-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="8fd09-150">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-150">string</span></span>|<span data-ttu-id="8fd09-151">Olá relativo toochange Olá nome e o email para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-151">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="8fd09-152">canChangePassword</span></span>|<span data-ttu-id="8fd09-153">Booliano</span><span class="sxs-lookup"><span data-stu-id="8fd09-153">boolean</span></span>|<span data-ttu-id="8fd09-154">Se o usuário atual Olá pode alterar sua senha.</span><span class="sxs-lookup"><span data-stu-id="8fd09-154">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="8fd09-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="8fd09-155">isSystemUser</span></span>|<span data-ttu-id="8fd09-156">Booliano</span><span class="sxs-lookup"><span data-stu-id="8fd09-156">boolean</span></span>|<span data-ttu-id="8fd09-157">Se o usuário atual Olá é um membro de uma das interno de saudação [grupos](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="8fd09-157">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="8fd09-158">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="8fd09-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="8fd09-159"><a name="Subscriptions"></a> Assinaturas</span><span class="sxs-lookup"><span data-stu-id="8fd09-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="8fd09-160">Olá **assinaturas** modelo permite que você toocustomize seção de assinaturas de saudação da página de perfil de usuário Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-160">hello **Subscriptions** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8fd09-161">![Página de assinatura de usuário](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Página de assinatura de usuário do APIM")</span><span class="sxs-lookup"><span data-stu-id="8fd09-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8fd09-162">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="8fd09-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="8fd09-163">Controles</span><span class="sxs-lookup"><span data-stu-id="8fd09-163">Controls</span></span>  
 <span data-ttu-id="8fd09-164">Esse modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="8fd09-164">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="8fd09-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="8fd09-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="8fd09-166">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="8fd09-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8fd09-167">Olá [perfil](#Profile), [aplicativos](#Applications), e [assinaturas](#Subscriptions) modelos compartilham Olá mesmo dados modelam e recebem Olá mesmos dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="8fd09-167">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="8fd09-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8fd09-168">Property</span></span>|<span data-ttu-id="8fd09-169">Tipo</span><span class="sxs-lookup"><span data-stu-id="8fd09-169">Type</span></span>|<span data-ttu-id="8fd09-170">Descrição</span><span class="sxs-lookup"><span data-stu-id="8fd09-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="8fd09-171">firstName</span><span class="sxs-lookup"><span data-stu-id="8fd09-171">firstName</span></span>|<span data-ttu-id="8fd09-172">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-172">string</span></span>|<span data-ttu-id="8fd09-173">Nome do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-173">First name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-174">lastName</span><span class="sxs-lookup"><span data-stu-id="8fd09-174">lastName</span></span>|<span data-ttu-id="8fd09-175">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-175">string</span></span>|<span data-ttu-id="8fd09-176">Sobrenome do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-176">Last name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-177">companyName</span><span class="sxs-lookup"><span data-stu-id="8fd09-177">companyName</span></span>|<span data-ttu-id="8fd09-178">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-178">string</span></span>|<span data-ttu-id="8fd09-179">nome da empresa do usuário atual Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="8fd09-179">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="8fd09-180">addresserEmail</span></span>|<span data-ttu-id="8fd09-181">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-181">string</span></span>|<span data-ttu-id="8fd09-182">Endereço de email do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-182">Email address of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="8fd09-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="8fd09-184">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-184">string</span></span>|<span data-ttu-id="8fd09-185">Análise de tooview de URL relativo para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-185">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="8fd09-186">subscriptions</span></span>|<span data-ttu-id="8fd09-187">Coleção de entidades de [Assinatura](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="8fd09-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="8fd09-188">assinaturas de saudação para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-188">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-189">de dimensionamento da Web</span><span class="sxs-lookup"><span data-stu-id="8fd09-189">applications</span></span>|<span data-ttu-id="8fd09-190">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="8fd09-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="8fd09-191">aplicativos de saudação do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-191">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="8fd09-192">changePasswordUrl</span></span>|<span data-ttu-id="8fd09-193">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-193">string</span></span>|<span data-ttu-id="8fd09-194">Olá relativo URL toochange Olá senha do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="8fd09-194">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="8fd09-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="8fd09-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="8fd09-196">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-196">string</span></span>|<span data-ttu-id="8fd09-197">Olá relativo toochange Olá nome e o email para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-197">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="8fd09-198">canChangePassword</span></span>|<span data-ttu-id="8fd09-199">Booliano</span><span class="sxs-lookup"><span data-stu-id="8fd09-199">boolean</span></span>|<span data-ttu-id="8fd09-200">Se o usuário atual Olá pode alterar sua senha.</span><span class="sxs-lookup"><span data-stu-id="8fd09-200">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="8fd09-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="8fd09-201">isSystemUser</span></span>|<span data-ttu-id="8fd09-202">Booliano</span><span class="sxs-lookup"><span data-stu-id="8fd09-202">boolean</span></span>|<span data-ttu-id="8fd09-203">Se o usuário atual Olá é um membro de uma das interno de saudação [grupos](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="8fd09-203">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="8fd09-204">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="8fd09-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="8fd09-205"><a name="Applications"></a> Aplicativos</span><span class="sxs-lookup"><span data-stu-id="8fd09-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="8fd09-206">Olá **aplicativos** modelo permite que você toocustomize seção de assinaturas de saudação da página de perfil de usuário Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-206">hello **Applications** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8fd09-207">![Página Aplicativos da conta de usuário](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Página Aplicativos da conta de usuário de APIM")</span><span class="sxs-lookup"><span data-stu-id="8fd09-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8fd09-208">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="8fd09-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="8fd09-209">Controles</span><span class="sxs-lookup"><span data-stu-id="8fd09-209">Controls</span></span>  
 <span data-ttu-id="8fd09-210">Esse modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="8fd09-210">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="8fd09-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="8fd09-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="8fd09-212">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="8fd09-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8fd09-213">Olá [perfil](#Profile), [aplicativos](#Applications), e [assinaturas](#Subscriptions) modelos compartilham Olá mesmo dados modelam e recebem Olá mesmos dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="8fd09-213">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="8fd09-214">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8fd09-214">Property</span></span>|<span data-ttu-id="8fd09-215">Tipo</span><span class="sxs-lookup"><span data-stu-id="8fd09-215">Type</span></span>|<span data-ttu-id="8fd09-216">Descrição</span><span class="sxs-lookup"><span data-stu-id="8fd09-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="8fd09-217">firstName</span><span class="sxs-lookup"><span data-stu-id="8fd09-217">firstName</span></span>|<span data-ttu-id="8fd09-218">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-218">string</span></span>|<span data-ttu-id="8fd09-219">Nome do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-219">First name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-220">lastName</span><span class="sxs-lookup"><span data-stu-id="8fd09-220">lastName</span></span>|<span data-ttu-id="8fd09-221">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-221">string</span></span>|<span data-ttu-id="8fd09-222">Sobrenome do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-222">Last name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-223">companyName</span><span class="sxs-lookup"><span data-stu-id="8fd09-223">companyName</span></span>|<span data-ttu-id="8fd09-224">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-224">string</span></span>|<span data-ttu-id="8fd09-225">nome da empresa do usuário atual Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="8fd09-225">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="8fd09-226">addresserEmail</span></span>|<span data-ttu-id="8fd09-227">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-227">string</span></span>|<span data-ttu-id="8fd09-228">Endereço de email do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-228">Email address of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="8fd09-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="8fd09-230">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-230">string</span></span>|<span data-ttu-id="8fd09-231">Análise de tooview de URL relativo para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-231">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="8fd09-232">subscriptions</span></span>|<span data-ttu-id="8fd09-233">Coleção de entidades de [Assinatura](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="8fd09-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="8fd09-234">assinaturas de saudação para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-234">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-235">de dimensionamento da Web</span><span class="sxs-lookup"><span data-stu-id="8fd09-235">applications</span></span>|<span data-ttu-id="8fd09-236">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="8fd09-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="8fd09-237">aplicativos de saudação do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-237">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="8fd09-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="8fd09-238">changePasswordUrl</span></span>|<span data-ttu-id="8fd09-239">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-239">string</span></span>|<span data-ttu-id="8fd09-240">Olá relativo URL toochange Olá senha do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="8fd09-240">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="8fd09-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="8fd09-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="8fd09-242">string</span><span class="sxs-lookup"><span data-stu-id="8fd09-242">string</span></span>|<span data-ttu-id="8fd09-243">Olá relativo toochange Olá nome e o email para o usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-243">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="8fd09-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="8fd09-244">canChangePassword</span></span>|<span data-ttu-id="8fd09-245">Booliano</span><span class="sxs-lookup"><span data-stu-id="8fd09-245">boolean</span></span>|<span data-ttu-id="8fd09-246">Se o usuário atual Olá pode alterar sua senha.</span><span class="sxs-lookup"><span data-stu-id="8fd09-246">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="8fd09-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="8fd09-247">isSystemUser</span></span>|<span data-ttu-id="8fd09-248">Booliano</span><span class="sxs-lookup"><span data-stu-id="8fd09-248">boolean</span></span>|<span data-ttu-id="8fd09-249">Se o usuário atual Olá é um membro de uma das interno de saudação [grupos](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="8fd09-249">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="8fd09-250">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="8fd09-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="8fd09-251"><a name="UpdateAccountInfo"></a> Atualizar informações da conta</span><span class="sxs-lookup"><span data-stu-id="8fd09-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="8fd09-252">Olá **Uodate as informações de conta** modelo permite Olá toocustomize **atualizar informações de conta** página no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="8fd09-252">hello **Uodate account info** template allows you toocustomize hello **Update account information** page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8fd09-253">![Modelos do portal do desenvolvedor da página de informações conta de usuário](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor da página de informações conta de usuário do APIM")</span><span class="sxs-lookup"><span data-stu-id="8fd09-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8fd09-254">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="8fd09-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="8fd09-255">Controles</span><span class="sxs-lookup"><span data-stu-id="8fd09-255">Controls</span></span>  
 <span data-ttu-id="8fd09-256">Este modelo pode não usar nenhum [controle de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="8fd09-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="8fd09-257">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="8fd09-257">Data model</span></span>  
 <span data-ttu-id="8fd09-258">Entidade [Informações de conta de usuário](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="8fd09-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="8fd09-259">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="8fd09-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="8fd09-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fd09-260">Next steps</span></span>
<span data-ttu-id="8fd09-261">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8fd09-261">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
