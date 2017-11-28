---
title: "aaaHow toouse hello Azure SDK de aplicativos móveis para Android | Microsoft Docs"
description: "Como toouse Olá SDK de aplicativos móveis do Azure para Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="1ef90-103">Como toouse Olá SDK de aplicativos móveis do Azure para Android</span><span class="sxs-lookup"><span data-stu-id="1ef90-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="1ef90-104">Este guia mostra como toouse Olá Android SDK de cliente para cenários comuns de tooimplement de aplicativos móveis, como:</span><span class="sxs-lookup"><span data-stu-id="1ef90-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="1ef90-105">Consulta de dados (inserir, atualizar e excluir).</span><span class="sxs-lookup"><span data-stu-id="1ef90-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="1ef90-106">Autenticação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-106">Authentication.</span></span>
* <span data-ttu-id="1ef90-107">Tratamento de erros.</span><span class="sxs-lookup"><span data-stu-id="1ef90-107">Handling errors.</span></span>
* <span data-ttu-id="1ef90-108">Personalizando cliente hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-108">Customizing hello client.</span></span>

<span data-ttu-id="1ef90-109">Este guia se concentra na saudação do cliente SDK do Android.</span><span class="sxs-lookup"><span data-stu-id="1ef90-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="1ef90-110">toolearn mais sobre hello SDKs do lado do servidor para aplicativos móveis, consulte [trabalhar com o back-end .NET SDK] [ 10] ou [como toouse Olá back-end node. js SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="1ef90-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="1ef90-111">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="1ef90-111">Reference Documentation</span></span>

<span data-ttu-id="1ef90-112">Você pode encontrar hello [referência da API Javadocs] [ 12] para a biblioteca de cliente do Android Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="1ef90-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="1ef90-113">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="1ef90-113">Supported Platforms</span></span>

<span data-ttu-id="1ef90-114">Hello Azure SDK de aplicativos móveis para Android oferece suporte a API níveis 19 a 24 (KitKat por meio de Nougat) para formatos de telefone e tablet.</span><span class="sxs-lookup"><span data-stu-id="1ef90-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="1ef90-115">A autenticação, em particular, utiliza um credenciais de toogather abordagem do framework do web comuns.</span><span class="sxs-lookup"><span data-stu-id="1ef90-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="1ef90-116">A autenticação de fluxo do servidor não funciona com dispositivos de fator de forma pequeno como inspeções.</span><span class="sxs-lookup"><span data-stu-id="1ef90-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="1ef90-117">Configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ef90-117">Setup and Prerequisites</span></span>

<span data-ttu-id="1ef90-118">Olá completa [início rápido de aplicativos móveis](app-service-mobile-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ef90-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="1ef90-119">Essa tarefa faz com que todos os pré-requisitos para o desenvolvimento de Aplicativos Móveis do Azure sejam atendidos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="1ef90-120">Olá Quickstart também ajuda você a configurar sua conta e criar seu primeiro back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1ef90-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="1ef90-121">Se você decidir não toocomplete tutorial de início rápido de Olá, conclua Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ef90-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="1ef90-122">[criar um back-end do aplicativo móvel] [ 13] toouse com seu aplicativo do Android.</span><span class="sxs-lookup"><span data-stu-id="1ef90-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="1ef90-123">No Android Studio, [criar arquivos de atualização Olá Gradle](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="1ef90-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="1ef90-124">[Habilitar a permissão de Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="1ef90-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="1ef90-125"><a name="gradle-build"></a>Atualizar Olá Gradle criar arquivo</span><span class="sxs-lookup"><span data-stu-id="1ef90-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="1ef90-126">Altere ambos os arquivos **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="1ef90-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="1ef90-127">Adicione este código toohello *projeto* nível **gradle** arquivo hello *buildscript* marca:</span><span class="sxs-lookup"><span data-stu-id="1ef90-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="1ef90-128">Adicione este código toohello *aplicativo módulo* nível **gradle** arquivo hello *dependências* marca:</span><span class="sxs-lookup"><span data-stu-id="1ef90-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="1ef90-129">Atualmente a versão mais recente da saudação é 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="1ef90-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="1ef90-130">Olá suporte para as versões são listadas [na bintray][14].</span><span class="sxs-lookup"><span data-stu-id="1ef90-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="1ef90-131"><a name="enable-internet"></a>Habilitar a permissão de Internet</span><span class="sxs-lookup"><span data-stu-id="1ef90-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="1ef90-132">tooaccess do Azure, seu aplicativo deve ter permissão de INTERNET Olá habilitada.</span><span class="sxs-lookup"><span data-stu-id="1ef90-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="1ef90-133">Se ele ainda não estiver habilitado, adicionar Olá a seguinte linha de código tooyour **AndroidManifest.xml** arquivo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="1ef90-134">Criar uma conexão de cliente</span><span class="sxs-lookup"><span data-stu-id="1ef90-134">Create a Client Connection</span></span>

<span data-ttu-id="1ef90-135">Aplicativos móveis do Azure fornece quatro funções de aplicativo móvel tooyour:</span><span class="sxs-lookup"><span data-stu-id="1ef90-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="1ef90-136">Acesso a Dados e a Sincronização Offline com um Serviço de Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef90-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="1ef90-137">Chame APIs personalizado escrito com hello SDK de servidor de aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef90-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="1ef90-138">Autenticação com autenticação e autorização do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef90-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="1ef90-139">Envie notificações por push com hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="1ef90-140">Cada uma dessas funções primeiro exige que você crie um objeto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="1ef90-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="1ef90-141">Apenas um objeto `MobileServiceClient` deve ser criado em seu cliente móvel (ou seja, deve ser um padrão Singleton).</span><span class="sxs-lookup"><span data-stu-id="1ef90-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="1ef90-142">toocreate um `MobileServiceClient` objeto:</span><span class="sxs-lookup"><span data-stu-id="1ef90-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="1ef90-143">Olá `<MobileAppUrl>` é uma cadeia de caracteres ou um objeto de URL que aponta o back-end do tooyour móvel.</span><span class="sxs-lookup"><span data-stu-id="1ef90-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="1ef90-144">Se você estiver usando o serviço de aplicativo do Azure toohost seu back-end móvel, em seguida, certifique-se de usar Olá seguro `https://` versão da URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="1ef90-145">Olá cliente também exige acesso toohello atividade ou contexto - Olá `this` parâmetro no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="1ef90-146">Olá MobileServiceClient construção deve acontecer dentro de saudação `onCreate()` método hello atividade referenciada no hello `AndroidManifest.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="1ef90-147">Como prática recomendada, você deve abstrair a comunicação do servidor em sua própria classe (padrão singleton).</span><span class="sxs-lookup"><span data-stu-id="1ef90-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="1ef90-148">Nesse caso, você deve passar hello atividade dentro de saudação construtor tooappropriately Configurar serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="1ef90-149">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="1ef90-150">Agora você pode chamar `AzureServiceAdapter.Initialize(this);` em Olá `onCreate()` método de sua atividade principal.</span><span class="sxs-lookup"><span data-stu-id="1ef90-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="1ef90-151">Usam outros métodos que precisam de cliente de acesso à toohello `AzureServiceAdapter.getInstance();` tooobtain um adaptador de serviço de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="1ef90-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="1ef90-152">Operações de dados</span><span class="sxs-lookup"><span data-stu-id="1ef90-152">Data Operations</span></span>

<span data-ttu-id="1ef90-153">núcleo de saudação do hello SDK de aplicativos móveis do Azure é tooprovide acesso toodata armazenado no SQL Azure no back-end de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="1ef90-154">Você pode acessar esses dados usando classes fortemente tipadas (preferido) ou consultas não tipadas (não recomendado).</span><span class="sxs-lookup"><span data-stu-id="1ef90-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="1ef90-155">em massa de saudação desta seção lida com usando classes com rigidez de tipos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="1ef90-156">Definir as classes de dados do cliente</span><span class="sxs-lookup"><span data-stu-id="1ef90-156">Define client data classes</span></span>

<span data-ttu-id="1ef90-157">tooaccess dados de tabelas do SQL Azure, definir classes de dados do cliente que correspondem a tabelas toohello no back-end de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="1ef90-158">Exemplos neste tópico presumem uma tabela chamada **MyDataTable**, que tem Olá colunas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ef90-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="1ef90-159">ID</span><span class="sxs-lookup"><span data-stu-id="1ef90-159">id</span></span>
* <span data-ttu-id="1ef90-160">text</span><span class="sxs-lookup"><span data-stu-id="1ef90-160">text</span></span>
* <span data-ttu-id="1ef90-161">concluído</span><span class="sxs-lookup"><span data-stu-id="1ef90-161">complete</span></span>

<span data-ttu-id="1ef90-162">Olá correspondente com tipo do lado do cliente objeto reside em um arquivo chamado **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="1ef90-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="1ef90-163">Adicione os métodos getter e setter para cada campo que você adicionar.</span><span class="sxs-lookup"><span data-stu-id="1ef90-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="1ef90-164">Se sua tabela do SQL Azure contém mais colunas, você poderia adicionar classe de toothis de campos correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="1ef90-165">Por exemplo, se hello DTO (objeto de transferência de dados) tiver uma coluna de prioridade de número inteiro, em seguida, você pode adicionar esse campo, junto com seus métodos getter e setter:</span><span class="sxs-lookup"><span data-stu-id="1ef90-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="1ef90-166">toolearn como toocreate outras tabelas no seu back-end de aplicativos móveis, consulte [como: definir um controlador de tabela] [ 15] (back-end .NET) ou [definir tabelas usando um esquema dinâmico] [ 16] (Node. js back-end).</span><span class="sxs-lookup"><span data-stu-id="1ef90-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="1ef90-167">Uma tabela de back-end os aplicativos móveis do Azure define cinco campos especiais, quatro delas são tooclients disponíveis:</span><span class="sxs-lookup"><span data-stu-id="1ef90-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="1ef90-168">`String id`: Olá ID globalmente exclusiva para registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="1ef90-169">Como uma prática recomendada, verifique a representação de cadeia de caracteres de Olá Olá id de um [UUID] [ 17] objeto.</span><span class="sxs-lookup"><span data-stu-id="1ef90-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="1ef90-170">`DateTimeOffset updatedAt`: Olá data/hora da última atualização do hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="1ef90-171">campo de updatedAt de saudação é definido pelo servidor de saudação e nunca deve ser definido por código do cliente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="1ef90-172">`DateTimeOffset createdAt`: data/hora Olá Olá objeto foi criado.</span><span class="sxs-lookup"><span data-stu-id="1ef90-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="1ef90-173">campo de criadona de saudação é definido pelo servidor de saudação e nunca deve ser definido por código do cliente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="1ef90-174">`byte[] version`: Normalmente é representada como uma cadeia de caracteres, versão Olá também é definido pelo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="1ef90-175">`boolean deleted`: Indica que registro Olá foi excluído, mas ainda não foi limpo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="1ef90-176">Não use `deleted` como uma propriedade em sua classe.</span><span class="sxs-lookup"><span data-stu-id="1ef90-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="1ef90-177">Olá `id` campo é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="1ef90-177">hello `id` field is required.</span></span>  <span data-ttu-id="1ef90-178">Olá `updatedAt` campo e `version` campo são usados para sincronização offline (para a resolução de conflito e de sincronização incremental respectivamente).</span><span class="sxs-lookup"><span data-stu-id="1ef90-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="1ef90-179">Olá `createdAt` campo é um campo de referência e não é usado pelo cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="1ef90-180">Olá nomes são "entre-the-wire" nomes de propriedades de saudação e não ajustáveis.</span><span class="sxs-lookup"><span data-stu-id="1ef90-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="1ef90-181">No entanto, você pode criar um mapeamento entre o objeto e hello nomes de "em-the-wire" usando Olá [gson] [ 3] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="1ef90-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="1ef90-182">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="1ef90-183">Criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="1ef90-183">Create a Table Reference</span></span>

<span data-ttu-id="1ef90-184">tooaccess uma tabela, primeiro crie um [MobileServiceTable] [ 8] objeto por chamada hello **getTable** método hello [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="1ef90-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="1ef90-185">Esse método tem duas sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="1ef90-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="1ef90-186">Em Olá seguindo o código, **mClient** é um objeto de MobileServiceClient de tooyour de referência.</span><span class="sxs-lookup"><span data-stu-id="1ef90-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="1ef90-187">sobrecarga primeiro Olá usada no qual o nome da classe hello e o nome da tabela de saudação serão Olá mesmo, e é hello um usado em Olá início rápido:</span><span class="sxs-lookup"><span data-stu-id="1ef90-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="1ef90-188">Olá segunda sobrecarga é usada quando o nome da tabela Olá é diferente do nome de classe Olá: Olá primeiro parâmetro é o nome da tabela hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="1ef90-189"><a name="query"></a>Consultar uma tabela de back-end</span><span class="sxs-lookup"><span data-stu-id="1ef90-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="1ef90-190">Primeiro, obtenha uma referência de tabela.</span><span class="sxs-lookup"><span data-stu-id="1ef90-190">First, obtain a table reference.</span></span>  <span data-ttu-id="1ef90-191">Em seguida, execute uma consulta na referência de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="1ef90-192">Uma consulta é qualquer combinação de:</span><span class="sxs-lookup"><span data-stu-id="1ef90-192">A query is any combination of:</span></span>

* <span data-ttu-id="1ef90-193">Uma [cláusula de filtro `.where()`](#filtering).</span><span class="sxs-lookup"><span data-stu-id="1ef90-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="1ef90-194">Uma [cláusula de ordenação `.orderBy()`](#sorting).</span><span class="sxs-lookup"><span data-stu-id="1ef90-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="1ef90-195">Uma [cláusula de seleção de campo `.select()`](#selection).</span><span class="sxs-lookup"><span data-stu-id="1ef90-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="1ef90-196">Um `.skip()` e `.top()` para [resultados paginados](#paging).</span><span class="sxs-lookup"><span data-stu-id="1ef90-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="1ef90-197">cláusulas Olá devem ser apresentadas em Olá anterior ordem.</span><span class="sxs-lookup"><span data-stu-id="1ef90-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="1ef90-198"><a name="filter"></a> Filtragem de resultados</span><span class="sxs-lookup"><span data-stu-id="1ef90-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="1ef90-199">saudação de forma geral de uma consulta é:</span><span class="sxs-lookup"><span data-stu-id="1ef90-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="1ef90-200">Olá, exemplo anterior retorna todos os resultados (o tamanho de página máximo toohello definido pelo servidor de saudação).</span><span class="sxs-lookup"><span data-stu-id="1ef90-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="1ef90-201">Olá `.execute()` método executa a consulta de saudação em Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="1ef90-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="1ef90-202">Olá, consulta é convertida tooan [OData v3] [ 19] consulta antes de back-end do transmissão toohello aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="1ef90-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="1ef90-203">Após o recebimento, back-end de aplicativos móveis Olá converte consulta Olá em uma instrução SQL antes de executá-lo na instância do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="1ef90-204">Desde que a atividade de rede leva algum tempo, Olá `.execute()` método retorna um [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="1ef90-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="1ef90-205"><a name="filtering"></a>Filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="1ef90-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="1ef90-206">Olá a execução da consulta a seguir retorna todos os itens de saudação **ToDoItem** tabela onde **completa** é igual a **false**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="1ef90-207">**mToDoTable** é Olá referência toohello serviço móvel tabela que criamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="1ef90-208">Definir um filtro usando Olá **onde** chamada de método na referência de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="1ef90-209">Olá **onde** método é seguido por um **campo** método seguido por um método que especifica um predicado de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="1ef90-210">Os possíveis métodos de predicado incluem **eq** (igual),**ne** (diferente), **gt** (maior que), **ge** (maior que ou igual a), **lt** (menor que), **le** (menor que ou igual a).</span><span class="sxs-lookup"><span data-stu-id="1ef90-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="1ef90-211">Esses métodos permitem que você compare o número e toospecific valores de campos de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1ef90-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="1ef90-212">Você pode filtrar por datas.</span><span class="sxs-lookup"><span data-stu-id="1ef90-212">You can filter on dates.</span></span> <span data-ttu-id="1ef90-213">Olá métodos a seguir permitem que você compare o campo de data inteiro do hello ou partes de data de saudação: **ano**, **mês**, **dia**, **hora**, **minuto**, e **segundo**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="1ef90-214">Olá, exemplo a seguir adiciona um filtro para itens cujos *data de vencimento* é igual a 2013.</span><span class="sxs-lookup"><span data-stu-id="1ef90-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="1ef90-215">Olá métodos a seguir suportam filtros complexos em campos de cadeia de caracteres: **startsWith**, **endsWith**, **concat**, **subcadeia de caracteres**, **indexOf**, **substituir**, **toLower**, **toUpper**, **trim**, e  **comprimento**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="1ef90-216">Olá filtros de exemplo a seguir para linhas de tabela onde hello *texto* coluna começa com "PRI0".</span><span class="sxs-lookup"><span data-stu-id="1ef90-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="1ef90-217">Olá métodos operadores a seguir têm suporte em campos de número: **adicionar**, **sub**, **mul**, **div**, **mod**, **andar**, **ceiling**, e **arredondar**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="1ef90-218">Olá filtros de exemplo a seguir para linhas de tabela onde hello **duração** é um número par.</span><span class="sxs-lookup"><span data-stu-id="1ef90-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="1ef90-219">É possível combinar predicados com estes métodos lógicos: **and**, **or** e **not**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="1ef90-220">saudação de exemplo a seguir combina duas Olá anterior exemplos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="1ef90-221">Agrupar e aninhar operadores lógicos:</span><span class="sxs-lookup"><span data-stu-id="1ef90-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="1ef90-222">Para obter mais exemplos de filtragem e uma discussão, consulte [explorando riqueza de saudação do modelo de consulta de cliente do Android Olá][20].</span><span class="sxs-lookup"><span data-stu-id="1ef90-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="1ef90-223"><a name="sorting"></a>Classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="1ef90-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="1ef90-224">Olá código a seguir retorna todos os itens de uma tabela de **ToDoItems** classificada em ordem crescente por Olá *texto* campo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="1ef90-225">*mToDoTable* é Olá referência toohello tabela de back-end que você criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1ef90-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="1ef90-226">Olá primeiro parâmetro da saudação **orderBy** método é um nome de toohello igual de cadeia de caracteres do campo Olá no qual toosort.</span><span class="sxs-lookup"><span data-stu-id="1ef90-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="1ef90-227">usa o segundo parâmetro de Olá Olá **QueryOrder** toospecify de enumeração se toosort em ordem crescente ou decrescente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="1ef90-228">Se você estiver filtrando usando Olá ***onde*** método, Olá ***onde*** método deve ser chamado antes de saudação ***orderBy*** método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="1ef90-229"><a name="selection"></a>Selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="1ef90-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="1ef90-230">Olá código a seguir ilustra como tooreturn todos os itens de uma tabela de **ToDoItems**, mas exibe apenas Olá **completa** e **texto** campos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="1ef90-231">**mToDoTable** é Olá referência toohello tabela de back-end que criamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="1ef90-232">função select do Hello parâmetros toohello são nomes de cadeia de caracteres de Olá Olá das colunas da tabela que você deseja tooreturn.</span><span class="sxs-lookup"><span data-stu-id="1ef90-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="1ef90-233">Olá **selecione** método precisa toofollow métodos como **onde** e **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="1ef90-234">Ele pode ser seguido por métodos de paginação como **skip** e **top**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="1ef90-235"><a name="paging"></a>Retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="1ef90-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="1ef90-236">Os dados **SEMPRE** retornam em páginas.</span><span class="sxs-lookup"><span data-stu-id="1ef90-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="1ef90-237">número máximo de saudação de registros retornados é definido pelo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="1ef90-238">Se cliente Olá solicitar mais registros, o servidor de saudação retorna o número máximo de saudação de registros.</span><span class="sxs-lookup"><span data-stu-id="1ef90-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="1ef90-239">Por padrão, o tamanho máximo da página de saudação no servidor de saudação é 50 registros.</span><span class="sxs-lookup"><span data-stu-id="1ef90-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="1ef90-240">Olá primeiro exemplo mostra como tooselect Olá primeiros cinco itens de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="1ef90-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="1ef90-241">consulta de saudação retorna os itens de saudação de uma tabela de **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="1ef90-242">**mToDoTable** é Olá referência toohello tabela de back-end que você criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1ef90-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="1ef90-243">Aqui está uma consulta que ignora Olá cinco primeiros itens e, em seguida, retorna Olá cinco Avançar:</span><span class="sxs-lookup"><span data-stu-id="1ef90-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="1ef90-244">Se você quiser tooget todos os registros em uma tabela, implemente o código tooiterate sobre todas as páginas:</span><span class="sxs-lookup"><span data-stu-id="1ef90-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="1ef90-245">Uma solicitação para todos os registros usando esse método cria um mínimo de back-end de aplicativos móveis de toohello duas solicitações.</span><span class="sxs-lookup"><span data-stu-id="1ef90-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="1ef90-246">Escolher tamanho de página direita Olá é um equilíbrio entre o uso de memória enquanto a solicitação hello está ocorrendo, o uso de largura de banda e atraso ao receber dados saudação completamente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="1ef90-247">padrão de saudação (50 registros) é adequado para todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="1ef90-248">Se você operar exclusivamente em dispositivos de memória maior, aumente o too500.</span><span class="sxs-lookup"><span data-stu-id="1ef90-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="1ef90-249">Encontramos esse tamanho de página Olá crescentes além 500 registra os resultados em problemas de memória grandes e atrasos inaceitáveis.</span><span class="sxs-lookup"><span data-stu-id="1ef90-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="1ef90-250"><a name="chaining"></a>Como concatenar métodos de consulta</span><span class="sxs-lookup"><span data-stu-id="1ef90-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="1ef90-251">métodos de saudação usados em consultas de tabelas de back-end podem ser concatenados.</span><span class="sxs-lookup"><span data-stu-id="1ef90-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="1ef90-252">Encadeamento consulta métodos permite que você tooselect a colunas específicas de linhas filtradas que são classificadas e paginável.</span><span class="sxs-lookup"><span data-stu-id="1ef90-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="1ef90-253">Você pode criar filtros lógicos complexos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-253">You can create complex logical filters.</span></span>  <span data-ttu-id="1ef90-254">Cada método de consulta retorna um objeto de consulta.</span><span class="sxs-lookup"><span data-stu-id="1ef90-254">Each query method returns a Query object.</span></span> <span data-ttu-id="1ef90-255">série de saudação tooend de métodos e consulta de execução realmente hello, chamada hello **executar** método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="1ef90-256">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="1ef90-257">Olá encadeados consulta métodos devem ser ordenados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1ef90-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="1ef90-258">Métodos de filtragem (**where**).</span><span class="sxs-lookup"><span data-stu-id="1ef90-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="1ef90-259">Métodos de classificação (**orderBy**).</span><span class="sxs-lookup"><span data-stu-id="1ef90-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="1ef90-260">Métodos de seleção (**select**).</span><span class="sxs-lookup"><span data-stu-id="1ef90-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="1ef90-261">Métodos de paginação (**skip** e **top**).</span><span class="sxs-lookup"><span data-stu-id="1ef90-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="1ef90-262"><a name="binding"></a>Interface do usuário toohello dados de ligação</span><span class="sxs-lookup"><span data-stu-id="1ef90-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="1ef90-263">A associação de dados envolve três componentes:</span><span class="sxs-lookup"><span data-stu-id="1ef90-263">Data binding involves three components:</span></span>

* <span data-ttu-id="1ef90-264">fonte de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="1ef90-264">hello data source</span></span>
* <span data-ttu-id="1ef90-265">layout da tela Hello</span><span class="sxs-lookup"><span data-stu-id="1ef90-265">hello screen layout</span></span>
* <span data-ttu-id="1ef90-266">adaptador de saudação que ties Olá dois juntos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="1ef90-267">Em nosso código de exemplo, retornamos dados saudação da tabela de Mobile aplicativos SQL Azure Olá **ToDoItem** em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="1ef90-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="1ef90-268">Essa atividade é um padrão comum para aplicativos de dados.</span><span class="sxs-lookup"><span data-stu-id="1ef90-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="1ef90-269">Consultas de banco de dados geralmente retornam uma coleção de linhas que Olá cliente obtém uma lista ou matriz.</span><span class="sxs-lookup"><span data-stu-id="1ef90-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="1ef90-270">Neste exemplo, a matriz de saudação é fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="1ef90-271">código de saudação especifica um layout de tela que define o modo de exibição de saudação de dados Olá que aparece no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="1ef90-272">Hello dois são associados com um adaptador, o que esse código é uma extensão da saudação **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="1ef90-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="1ef90-273"><a name="layout"></a>Definir Olá Layout</span><span class="sxs-lookup"><span data-stu-id="1ef90-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="1ef90-274">layout de saudação é definido por vários trechos de código XML.</span><span class="sxs-lookup"><span data-stu-id="1ef90-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="1ef90-275">Dado um layout existente, Olá código a seguir representa Olá **ListView** queremos toopopulate com nossos dados de servidor.</span><span class="sxs-lookup"><span data-stu-id="1ef90-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="1ef90-276">Em Olá precede o código, Olá *listitem* atributo especifica a id de saudação do layout de saudação para uma linha individual na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="1ef90-277">Esse código especifica uma caixa de seleção e seu texto associado e é instanciado uma vez para cada item na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="1ef90-278">Esse layout não exibe Olá **id** campo e um layout mais complexo deve especificar campos adicionais na exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="1ef90-279">Esse código está em Olá **row_list_to_do.xml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="1ef90-280"><a name="adapter"></a>Defina o adaptador de saudação</span><span class="sxs-lookup"><span data-stu-id="1ef90-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="1ef90-281">Como a fonte de dados de saudação do nosso exibição é uma matriz de **ToDoItem**, podemos subclasse nosso adaptador de um **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="1ef90-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="1ef90-282">Essa subclasse produz uma exibição para cada **ToDoItem** usando Olá **row_list_to_do** layout.</span><span class="sxs-lookup"><span data-stu-id="1ef90-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="1ef90-283">Em nosso código, definimos Olá seguindo a classe que é uma extensão da saudação **ArrayAdapter&lt;E&gt;**  classe:</span><span class="sxs-lookup"><span data-stu-id="1ef90-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="1ef90-284">Substituir adaptadores Olá **getView** método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="1ef90-285">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="1ef90-286">Criamos uma instância dessa classe em nossa atividade, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="1ef90-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="1ef90-287">Olá segundo parâmetro toohello ToDoItemAdapter construtor é um layout de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="1ef90-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="1ef90-288">Agora podemos pode instanciar Olá **ListView** e atribuir Olá adaptador toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="1ef90-289"><a name="use-adapter"></a>Use Olá adaptador tooBind toohello da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="1ef90-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="1ef90-290">Agora você está pronto toouse associação de dados.</span><span class="sxs-lookup"><span data-stu-id="1ef90-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="1ef90-291">Olá código a seguir mostra como tooget itens na tabela de saudação e preenchimentos Olá adaptador local com hello itens devolvido.</span><span class="sxs-lookup"><span data-stu-id="1ef90-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="1ef90-292">Chamar adaptador Olá sempre que modificar Olá **ToDoItem** tabela.</span><span class="sxs-lookup"><span data-stu-id="1ef90-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="1ef90-293">Como as modificações são feitas de registro em registro, você trata de uma única linha em vez de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="1ef90-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="1ef90-294">Quando você insere um item, chame Olá **adicionar** método Olá adaptador ativada; quando a exclusão, chame Olá **remover** método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="1ef90-295">Você pode encontrar um exemplo completo em Olá [projeto Quickstart Android][21].</span><span class="sxs-lookup"><span data-stu-id="1ef90-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="1ef90-296"><a name="inserting"></a>Inserir dados em Olá back-end</span><span class="sxs-lookup"><span data-stu-id="1ef90-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="1ef90-297">Criar uma instância da saudação *ToDoItem* de classe e defina suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="1ef90-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="1ef90-298">Em seguida, use **Insert ()** tooinsert um objeto:</span><span class="sxs-lookup"><span data-stu-id="1ef90-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="1ef90-299">Olá retornou correspondências de entidade inseridos na tabela de back-end hello, ID de saudação incluído e quaisquer outros valores de dados de saudação (como Olá `createdAt`, `updatedAt`, e `version` campos) definido no hello back-end.</span><span class="sxs-lookup"><span data-stu-id="1ef90-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="1ef90-300">As tabelas de Aplicativos Móveis exigem uma coluna de chave primária denominada **id**. Essa coluna deve ser uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1ef90-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="1ef90-301">valor padrão de Olá Olá da coluna de ID é um GUID.</span><span class="sxs-lookup"><span data-stu-id="1ef90-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="1ef90-302">Você pode fornecer outros valores exclusivos, como endereços de email ou nomes de usuário.</span><span class="sxs-lookup"><span data-stu-id="1ef90-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="1ef90-303">Quando um valor de ID de cadeia de caracteres não for fornecido para um registro inserido, Olá back-end gera um novo GUID.</span><span class="sxs-lookup"><span data-stu-id="1ef90-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="1ef90-304">Valores de ID de cadeia de caracteres fornecem Olá vantagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ef90-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="1ef90-305">IDs podem ser gerados sem fazer um banco de dados de toohello de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="1ef90-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="1ef90-306">Os registros são toomerge mais fácil de tabelas diferentes ou bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="1ef90-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="1ef90-307">Os valores de ID integram-se melhor à lógica de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="1ef90-308">Valores de ID de cadeia de caracteres são **OBRIGATÓRIOS** para suporte de sincronização offline.</span><span class="sxs-lookup"><span data-stu-id="1ef90-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="1ef90-309">Você não pode alterar uma Id quando ela é armazenada no banco de dados de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="1ef90-310"><a name="updating"></a>Atualizar dados em um aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="1ef90-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="1ef90-311">tooupdate dados em uma tabela, passar Olá novo objeto toohello **Update ()** método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="1ef90-312">Neste exemplo, *item* é uma referência tooa linha hello *ToDoItem* tabela que tenha sido tooit algumas alterações feitas.</span><span class="sxs-lookup"><span data-stu-id="1ef90-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="1ef90-313">saudação de linha com hello mesmo **id** é atualizada.</span><span class="sxs-lookup"><span data-stu-id="1ef90-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="1ef90-314"><a name="deleting"></a>Excluir dados em um aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="1ef90-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="1ef90-315">saudação de código a seguir mostra como toodelete dados de uma tabela especificando Olá objeto de dados.</span><span class="sxs-lookup"><span data-stu-id="1ef90-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="1ef90-316">Você também pode excluir um item especificando Olá **id** campo de saudação toodelete de linha.</span><span class="sxs-lookup"><span data-stu-id="1ef90-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="1ef90-317"><a name="lookup"></a>Pesquisar um item específico por ID</span><span class="sxs-lookup"><span data-stu-id="1ef90-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="1ef90-318">Pesquisar um item com um determinado **id** campo com hello **Lookup ()** método:</span><span class="sxs-lookup"><span data-stu-id="1ef90-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="1ef90-319"><a name="untyped"></a>Como trabalhar com dados não tipados</span><span class="sxs-lookup"><span data-stu-id="1ef90-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="1ef90-320">o modelo de programação sem tipo Hello proporciona controle exato sobre serialização JSON.</span><span class="sxs-lookup"><span data-stu-id="1ef90-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="1ef90-321">Há alguns cenários comuns em que você poderá toouse um modelo de programação sem tipo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="1ef90-322">Por exemplo, se a tabela de back-end contiver várias colunas e você só precisa de um subconjunto de colunas de saudação do tooreference.</span><span class="sxs-lookup"><span data-stu-id="1ef90-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="1ef90-323">modelo de tipo Hello requer toodefine todas as colunas de saudação definidas no back-end do hello aplicativos móveis em sua classe de dados.</span><span class="sxs-lookup"><span data-stu-id="1ef90-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="1ef90-324">A maioria das chamadas à API para acessar dados de saudação é semelhante toohello digitado chamadas de programação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="1ef90-325">Olá principal diferença é no modelo sem tipo hello invocar métodos em Olá **MobileServiceJsonTable** objeto, em vez da saudação **MobileServiceTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="1ef90-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="1ef90-326"><a name="json_instance"></a>Criar uma instância de uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="1ef90-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="1ef90-327">Toohello semelhante digitado modelo, você comece obtendo uma referência de tabela, mas nesse caso é um **MobileServicesJsonTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="1ef90-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="1ef90-328">Obter referência Olá Olá chamada **getTable** método em uma instância do cliente hello:</span><span class="sxs-lookup"><span data-stu-id="1ef90-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="1ef90-329">Depois de criar uma instância do hello **MobileServiceJsonTable**, ele tem praticamente Olá mesma API disponível como com o modelo de programação tipada hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="1ef90-330">Em alguns casos, os métodos de saudação levar um parâmetro sem tipo, em vez de um parâmetro de tipo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="1ef90-331"><a name="json_insert"></a>Inserir em uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="1ef90-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="1ef90-332">Olá mostrado no código a seguir como toodo uma inserção.</span><span class="sxs-lookup"><span data-stu-id="1ef90-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="1ef90-333">Olá, primeira etapa é toocreate uma [JsonObject][1], que faz parte da saudação [gson] [ 3] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="1ef90-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="1ef90-334">Em seguida, Use **Insert ()** tooinsert Olá sem tipo objeto tabela hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="1ef90-335">Se você precisar tooget Olá ID de objeto Olá inserido, use Olá **getAsJsonPrimitive()** método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="1ef90-336"><a name="json_delete"></a>Excluir de uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="1ef90-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="1ef90-337">Olá código a seguir mostra como toodelete uma instância, Olá nesse caso, a mesma instância de um **JsonObject** que foi criado no antes da saudação *inserir* exemplo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="1ef90-338">código de saudação é hello igual Olá digitados caso, mas o método hello tem uma assinatura diferente, pois ela faz referência a um **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="1ef90-339">Você também pode excluir uma instância diretamente, usando sua ID:</span><span class="sxs-lookup"><span data-stu-id="1ef90-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="1ef90-340"><a name="json_get"></a>Retornar todas as linhas de uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="1ef90-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="1ef90-341">Olá mostrado no código a seguir como tooretrieve uma tabela inteira.</span><span class="sxs-lookup"><span data-stu-id="1ef90-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="1ef90-342">Como você está usando uma tabela de JSON, você pode recuperar apenas algumas das colunas da tabela Olá seletivamente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="1ef90-343">Olá a mesmo conjunto de filtragem, filtragem e paginação métodos que estão disponíveis para o modelo de tipo hello estão disponíveis para o modelo sem tipo hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="1ef90-344"><a name="offline-sync"></a>Implementar a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="1ef90-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="1ef90-345">Olá SDK de cliente de aplicativos móveis do Azure também implementa sincronização offline de dados usando um toostore de banco de dados SQLite uma cópia dos dados do servidor de saudação localmente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="1ef90-346">Operações executadas em uma tabela offline não exigem conectividade móvel toowork.</span><span class="sxs-lookup"><span data-stu-id="1ef90-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="1ef90-347">Sincronização offline ajuda a resiliência e desempenho a despesa de saudação de lógica mais complexa para resolução de conflitos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="1ef90-348">Olá SDK de cliente de aplicativos móveis do Azure implementa Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ef90-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="1ef90-349">Sincronização Incremental: somente registros novos e atualizados são baixados, economizando o consumo de largura de banda e de memória.</span><span class="sxs-lookup"><span data-stu-id="1ef90-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="1ef90-350">Simultaneidade otimista: Operações são consideradas toosucceed.</span><span class="sxs-lookup"><span data-stu-id="1ef90-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="1ef90-351">Resolução de conflitos é adiada até que as atualizações são executadas no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="1ef90-352">Resolução de conflito: Olá que SDK detecta quando uma alteração conflitante foi feita no servidor de saudação e fornece conecta o usuário de saudação tooalert.</span><span class="sxs-lookup"><span data-stu-id="1ef90-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="1ef90-353">Exclusão reversível: Registros excluídos são marcadas como excluídos, permitindo que outros dispositivos tooupdate seu cache offline.</span><span class="sxs-lookup"><span data-stu-id="1ef90-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="1ef90-354">Inicializar a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="1ef90-354">Initialize Offline Sync</span></span>

<span data-ttu-id="1ef90-355">Cada tabela offline deve ser definida no cache offline de saudação antes do uso.</span><span class="sxs-lookup"><span data-stu-id="1ef90-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="1ef90-356">Normalmente, a definição da tabela é feita imediatamente após a criação de saudação do cliente hello:</span><span class="sxs-lookup"><span data-stu-id="1ef90-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="1ef90-357">Obter uma referência toohello tabela de Cache Offline</span><span class="sxs-lookup"><span data-stu-id="1ef90-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="1ef90-358">Para uma tabela online, use `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="1ef90-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="1ef90-359">Para uma tabela offline, use `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="1ef90-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="1ef90-360">Todos os Olá métodos que estão disponíveis para tabelas online (incluindo a filtragem, classificação, paginação, inserção de dados, atualização de dados e exclusão de dados) funcionam igualmente bem em tabelas online e offline.</span><span class="sxs-lookup"><span data-stu-id="1ef90-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="1ef90-361">Sincronizar Olá Local Cache Offline</span><span class="sxs-lookup"><span data-stu-id="1ef90-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="1ef90-362">A sincronização é dentro do controle de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="1ef90-363">Veja um exemplo de método de sincronização:</span><span class="sxs-lookup"><span data-stu-id="1ef90-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="1ef90-364">Se um nome de consulta é fornecido toohello `.pull(query, queryname)` método e, em seguida, a sincronização incremental é usado tooreturn somente os registros que foram criados ou alterados desde a recepção de saudação última concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="1ef90-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="1ef90-365">Lidar com conflitos durante a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="1ef90-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="1ef90-366">Se um conflito ocorrer durante uma operação `.push()`, uma `MobileServiceConflictException` será lançada.</span><span class="sxs-lookup"><span data-stu-id="1ef90-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="1ef90-367">item de servidor emitido Olá é inserido na exceção de saudação e pode ser recuperada por `.getItem()` na exceção de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="1ef90-368">Ajuste push Olá por chamada hello itens a seguir no objeto de MobileServiceSyncContext hello:</span><span class="sxs-lookup"><span data-stu-id="1ef90-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="1ef90-369">Depois que todos os conflitos são marcados como quiser, chame `.push()` novamente tooresolve Olá a todos os conflitos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="1ef90-370"><a name="custom-api"></a>Chamar uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="1ef90-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="1ef90-371">Uma API personalizada permite que você toodefine pontos de extremidade personalizados que expõem a funcionalidade do servidor que não mapeiam tooan inserir, atualizar, excluir ou operação de leitura.</span><span class="sxs-lookup"><span data-stu-id="1ef90-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="1ef90-372">Usando uma API personalizada, você pode ter mais controle sobre mensagens, incluindo ler e definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem diferente do JSON.</span><span class="sxs-lookup"><span data-stu-id="1ef90-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="1ef90-373">Em um cliente Android, você chamar hello **invokeApi** método toocall Olá API ponto de extremidade personalizado.</span><span class="sxs-lookup"><span data-stu-id="1ef90-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="1ef90-374">Olá exemplo a seguir mostra como toocall um ponto de extremidade de API nomeados **completeAll**, que retorna uma classe de coleção chamada **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="1ef90-375">Olá **invokeApi** método é chamado no cliente de saudação, que envia uma mensagem de solicitação toohello nova API personalizada.</span><span class="sxs-lookup"><span data-stu-id="1ef90-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="1ef90-376">resultado de saudação retornado pela API personalizada Olá é exibido em uma caixa de diálogo de mensagem, como erros.</span><span class="sxs-lookup"><span data-stu-id="1ef90-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="1ef90-377">Outras versões do **invokeApi** permitem que você enviar um objeto no corpo da solicitação de saudação opcionalmente, especifique o método hello HTTP e enviar parâmetros de consulta com a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="1ef90-378">Versões não tipadas de **invokeApi** também são fornecidas.</span><span class="sxs-lookup"><span data-stu-id="1ef90-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="1ef90-379"><a name="authentication"></a>Adicionar autenticação tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="1ef90-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="1ef90-380">Tutoriais já descrevem detalhadamente como tooadd esses recursos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="1ef90-381">O Serviço de Aplicativo oferece suporte à [autenticação de usuários do aplicativo](app-service-mobile-android-get-started-users.md) usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft, Twitter e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ef90-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="1ef90-382">Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários.</span><span class="sxs-lookup"><span data-stu-id="1ef90-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="1ef90-383">Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização em seu back-end.</span><span class="sxs-lookup"><span data-stu-id="1ef90-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="1ef90-384">Dois fluxos de autenticação são suportados: um **server** flow e um **client** flow.</span><span class="sxs-lookup"><span data-stu-id="1ef90-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="1ef90-385">fluxo do servidor de saudação fornece experiência de autenticação mais simples de hello, como ele se baseia na interface de web de provedores de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="1ef90-386">Nenhum SDKs adicionais são necessárias tooimplement autenticação de fluxo do servidor.</span><span class="sxs-lookup"><span data-stu-id="1ef90-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="1ef90-387">Autenticação do servidor fluxo não oferece uma integração profunda no dispositivo móvel hello e só é recomendada para uma prova de cenários de conceito.</span><span class="sxs-lookup"><span data-stu-id="1ef90-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="1ef90-388">fluxo de saudação do cliente permite uma integração mais profunda com recursos específicos do dispositivo, como o logon único conforme depende dos SDKs fornecidos pelo provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="1ef90-389">Por exemplo, você pode integrar Olá Facebook SDK em seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1ef90-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="1ef90-390">cliente móvel Olá alterna para o aplicativo do Facebook hello e confirma o logon antes de trocá aplicativo móvel tooyour back.</span><span class="sxs-lookup"><span data-stu-id="1ef90-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="1ef90-391">Quatro etapas são necessárias tooenable autenticação em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="1ef90-392">Registrar o aplicativo para autenticação com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="1ef90-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="1ef90-393">Configurar o back-end do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="1ef90-394">Restringe os usuários de tooauthenticated de permissões de tabela somente em Olá back-end do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="1ef90-395">Adicione o aplicativo de tooyour de código de autenticação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="1ef90-396">Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários.</span><span class="sxs-lookup"><span data-stu-id="1ef90-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="1ef90-397">Você também pode usar o hello SID de um usuário autenticado toomodify solicitações.</span><span class="sxs-lookup"><span data-stu-id="1ef90-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="1ef90-398">Para obter mais informações, consulte [Introdução à autenticação] e hello documentação como de SDK do servidor.</span><span class="sxs-lookup"><span data-stu-id="1ef90-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="1ef90-399"><a name="caching"></a>Autenticação: Fluxo de servidor</span><span class="sxs-lookup"><span data-stu-id="1ef90-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="1ef90-400">Olá código a seguir inicia um processo de logon do fluxo de servidor usando o provedor de saudação do Google.</span><span class="sxs-lookup"><span data-stu-id="1ef90-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="1ef90-401">Configuração adicional é necessária devido aos requisitos de segurança Olá para o provedor de saudação do Google:</span><span class="sxs-lookup"><span data-stu-id="1ef90-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="1ef90-402">Além disso, adicione Olá classe principal de atividade do método toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ef90-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="1ef90-403">Olá `GOOGLE_LOGIN_REQUEST_CODE` definido na sua principal atividade é usada para Olá `login()` método e dentro de saudação `onActivityResult()` método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="1ef90-404">Você pode escolher qualquer número exclusivo, como hello mesmo número é usado em Olá `login()` método e hello `onActivityResult()` método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="1ef90-405">Se você abstrair o código de saudação do cliente em um adaptador de serviço (conforme mostrado anteriormente), você deve chamar métodos apropriados Olá no adaptador de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="1ef90-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="1ef90-406">Também é necessário um projeto de saudação tooconfigure para customtabs.</span><span class="sxs-lookup"><span data-stu-id="1ef90-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="1ef90-407">Primeiro, especifique uma URL de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="1ef90-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="1ef90-408">Adicionar Olá trecho de código a seguir muito`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="1ef90-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="1ef90-409">Adicionar Olá **redirectUriScheme** toohello `build.gradle` arquivo para seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="1ef90-410">Finalmente, adicione `com.android.support:customtabs:23.0.1` toohello lista de dependências no hello `build.gradle` arquivo:</span><span class="sxs-lookup"><span data-stu-id="1ef90-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="1ef90-411">Obter ID de saudação do hello usuário que fez logon de um **MobileServiceUser** usando Olá **getUserId** método.</span><span class="sxs-lookup"><span data-stu-id="1ef90-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="1ef90-412">Para obter um exemplo de como toouse futuros toocall Olá logon assíncrona APIs, consulte [Introdução à autenticação].</span><span class="sxs-lookup"><span data-stu-id="1ef90-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="1ef90-413">Olá mencionado o esquema de URL diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1ef90-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="1ef90-414">Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` tenham as mesmas maiúsculas ou minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1ef90-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="1ef90-415"><a name="caching"></a>Armazenar tokens de autenticação em cache</span><span class="sxs-lookup"><span data-stu-id="1ef90-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="1ef90-416">Cache de tokens de autenticação requer toostore Olá ID de usuário e token de autenticação localmente no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="1ef90-417">Hello próxima inicialização aplicativo hello, você verificará Olá cache, e se esses valores estiverem presentes, você pode ignorar log Olá no procedimento e realimentar cliente Olá com esses dados.</span><span class="sxs-lookup"><span data-stu-id="1ef90-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="1ef90-418">No entanto, esses dados são confidenciais e devem ser armazenado criptografados para segurança no caso de telefone Olá for roubado.</span><span class="sxs-lookup"><span data-stu-id="1ef90-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="1ef90-419">Você pode ver um exemplo completo de como os tokens de autenticação toocache em [seção de tokens de autenticação de Cache][7].</span><span class="sxs-lookup"><span data-stu-id="1ef90-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="1ef90-420">Quando você tenta toouse um token expirado, você receberá um *401 não autorizado* resposta.</span><span class="sxs-lookup"><span data-stu-id="1ef90-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="1ef90-421">Você pode tratar erros de autenticação usando filtros.</span><span class="sxs-lookup"><span data-stu-id="1ef90-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="1ef90-422">Filtros interceptam solicitações toohello back-end do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="1ef90-423">Olá filtro código testa resposta Olá para um 401, dispara o processo de entrada hello e recomeça a solicitação Olá que gerou Olá 401.</span><span class="sxs-lookup"><span data-stu-id="1ef90-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="1ef90-424"><a name="refresh"></a>Usar tokens de atualização</span><span class="sxs-lookup"><span data-stu-id="1ef90-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="1ef90-425">o token de saudação retornado por autorização e autenticação do serviço de aplicativo do Azure tem um tempo de vida definido de uma hora.</span><span class="sxs-lookup"><span data-stu-id="1ef90-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="1ef90-426">Após esse período, você deve autenticar novamente usuário hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="1ef90-427">Se você estiver usando um token de vida longa que você recebeu por meio de autenticação de cliente de fluxo, em seguida, você pode autenticar novamente com a autenticação do serviço de aplicativo do Azure e autorização Olá mesmo token.</span><span class="sxs-lookup"><span data-stu-id="1ef90-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="1ef90-428">Outro token de Serviço de Aplicativo do Azure é gerado com um novo tempo de vida.</span><span class="sxs-lookup"><span data-stu-id="1ef90-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="1ef90-429">Você também pode registrar Olá provedor toouse Tokens de atualização.</span><span class="sxs-lookup"><span data-stu-id="1ef90-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="1ef90-430">Nem sempre um token de atualização está disponível.</span><span class="sxs-lookup"><span data-stu-id="1ef90-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="1ef90-431">É necessário realizar uma configuração adicional:</span><span class="sxs-lookup"><span data-stu-id="1ef90-431">Additional configuration is required:</span></span>

* <span data-ttu-id="1ef90-432">Para **Active Directory do Azure**, configure um segredo do cliente para Olá aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ef90-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="1ef90-433">Especifica o segredo de cliente de Olá em saudação do serviço de aplicativo do Azure ao configurar a autenticação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef90-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="1ef90-434">Ao chamar `.login()`, passe `response_type=code id_token` como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="1ef90-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="1ef90-435">Para **Google**, passar Olá `access_type=offline` como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="1ef90-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="1ef90-436">Para **Microsoft Account**, selecione Olá `wl.offline_access` escopo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="1ef90-437">toorefresh um token, chame `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="1ef90-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="1ef90-438">Como prática recomendada, crie um filtro que detecta uma resposta 401 do servidor de saudação e tenta token de usuário toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="1ef90-439">Faça logon com a autenticação de cliente-fluxo</span><span class="sxs-lookup"><span data-stu-id="1ef90-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="1ef90-440">processo geral de saudação para registro em log com autenticação de cliente de fluxo é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1ef90-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="1ef90-441">Configure a Autenticação e Autorização do Serviço de Aplicativo do Azure como você faria com autenticação de servidor-fluxo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="1ef90-442">Integre o provedor de autenticação de saudação SDK para autenticação tooproduce um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="1ef90-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="1ef90-443">Chamar hello `.login()` método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1ef90-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="1ef90-444">Substituir saudação `onSuccess()` método com qualquer código que você deseja toouse em um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="1ef90-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="1ef90-445">Olá `{provider}` cadeia de caracteres é um provedor válido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, ou **twitter**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="1ef90-446">Se você tiver implementado autenticação personalizada, você também pode usar o marca de provedor de autenticação personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="1ef90-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="1ef90-447"><a name="adal"></a>Autenticar usuários com hello biblioteca de autenticação do Active Directory (ADAL)</span><span class="sxs-lookup"><span data-stu-id="1ef90-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="1ef90-448">Você pode usar usuários do hello biblioteca de autenticação do Active Directory (ADAL) toosign em seu aplicativo usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef90-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="1ef90-449">Usando um logon de fluxo de cliente geralmente é preferível toousing Olá `loginAsync()` métodos como ele fornece uma aparência UX mais nativa e permite a personalização adicional.</span><span class="sxs-lookup"><span data-stu-id="1ef90-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="1ef90-450">Configurar seu back-end do aplicativo móvel para entrar no AAD pela seguinte Olá [como tooconfigure aplicativo de serviço de logon do Active Directory] [ 22] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ef90-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="1ef90-451">Torne-se toocomplete Olá opcional de registro de um aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="1ef90-452">Instale o ADAL modificando a saudação de tooinclude de arquivo gradle definições a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ef90-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="1ef90-453">Adicione Olá aplicativo tooyour de código a seguir, tornando Olá substituições a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ef90-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="1ef90-454">Substituir **aqui de autoridade de inserção** com o nome de saudação do locatário Olá no qual você provisionou o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="1ef90-455">formato de saudação deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1ef90-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="1ef90-456">Substituir **inserir recursos-ID aqui** com a ID de cliente Olá para o back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1ef90-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="1ef90-457">Você pode obter a ID do cliente Olá de Olá **avançado** guia **configurações do Active Directory do Azure** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="1ef90-458">Substituir **aqui INSERT-CLIENT-ID** com a ID de cliente Olá você copiou do aplicativo cliente nativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="1ef90-459">Substituir **INSERT-REDIRECT-URI-aqui** com seu site */.auth/login/done* ponto de extremidade, usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1ef90-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="1ef90-460">Esse valor deve ser semelhante muito*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="1ef90-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="1ef90-461"><a name="filters"></a>Ajustar Olá comunicação cliente-servidor</span><span class="sxs-lookup"><span data-stu-id="1ef90-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="1ef90-462">saudação de conexão do cliente é normalmente uma conexão HTTP básica usando Olá subjacente biblioteca HTTP fornecida com hello SDK do Android.</span><span class="sxs-lookup"><span data-stu-id="1ef90-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="1ef90-463">Há várias razões por que você usaria toochange que:</span><span class="sxs-lookup"><span data-stu-id="1ef90-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="1ef90-464">Você deseja toouse um tempo limite alternativo tooadjust de biblioteca HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ef90-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="1ef90-465">Você deseja tooprovide uma barra de progresso.</span><span class="sxs-lookup"><span data-stu-id="1ef90-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="1ef90-466">Você deseja tooadd uma funcionalidade de gerenciamento do cabeçalho personalizado toosupport API.</span><span class="sxs-lookup"><span data-stu-id="1ef90-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="1ef90-467">Você deseja toointercept uma resposta com falha para que você possa implementar reautenticação.</span><span class="sxs-lookup"><span data-stu-id="1ef90-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="1ef90-468">Você deseja toolog solicitações de back-end tooan serviço de análise.</span><span class="sxs-lookup"><span data-stu-id="1ef90-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="1ef90-469">Usar uma biblioteca HTTP alternativa</span><span class="sxs-lookup"><span data-stu-id="1ef90-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="1ef90-470">Chamar hello `.setAndroidHttpClientFactory()` método imediatamente depois de criar sua referência de cliente.</span><span class="sxs-lookup"><span data-stu-id="1ef90-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="1ef90-471">Por exemplo, tooset Olá conexão timeout too60 segundos (em vez de padrão de saudação 10 segundos):</span><span class="sxs-lookup"><span data-stu-id="1ef90-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="1ef90-472">Implementar um filtro de progresso</span><span class="sxs-lookup"><span data-stu-id="1ef90-472">Implement a Progress Filter</span></span>

<span data-ttu-id="1ef90-473">Você pode implementar uma interceptação de cada solicitação implementando um `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="1ef90-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="1ef90-474">Por exemplo, o seguinte Olá atualiza uma barra de progresso pré-criados:</span><span class="sxs-lookup"><span data-stu-id="1ef90-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="1ef90-475">Você pode anexar este cliente toohello de filtro da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1ef90-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="1ef90-476">Personalizar cabeçalhos de solicitações</span><span class="sxs-lookup"><span data-stu-id="1ef90-476">Customize Request Headers</span></span>

<span data-ttu-id="1ef90-477">Use Olá seguinte `ServiceFilter` e anexe o filtro de saudação em Olá mesma maneira que Olá `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="1ef90-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="1ef90-478"><a name="conversions"></a>Configurar a Serialização Automática</span><span class="sxs-lookup"><span data-stu-id="1ef90-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="1ef90-479">Você pode especificar uma estratégia de conversão que aplica-se a coluna tooevery usando Olá [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="1ef90-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="1ef90-480">biblioteca de cliente do Android Olá usa [gson] [ 3] em segundo plano do hello tooserialize Java objetos tooJSON dados antes de dados saudação são enviados tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="1ef90-481">Olá, código a seguir usa Olá **setFieldNamingStrategy()** estratégia de saudação do método tooset.</span><span class="sxs-lookup"><span data-stu-id="1ef90-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="1ef90-482">Este exemplo exclui caractere inicial da saudação (um "m") e em letras minúsculas, em seguida, Olá próximo caractere, para cada nome de campo.</span><span class="sxs-lookup"><span data-stu-id="1ef90-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="1ef90-483">Por exemplo, ele poderia transformar "mId" em "id".</span><span class="sxs-lookup"><span data-stu-id="1ef90-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="1ef90-484">Implementar uma saudação de tooreduce de estratégia de conversão precisa para `SerializedName()` anotações na maioria dos campos.</span><span class="sxs-lookup"><span data-stu-id="1ef90-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="1ef90-485">Esse código deve ser executado antes de criar uma referência de cliente móvel usando Olá **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="1ef90-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[Introdução à autenticação]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
