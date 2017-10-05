---
title: "Como usar o SDK de Aplicativos Móveis do Azure para Android | Microsoft Docs"
description: "Como usar o SDK de Aplicativos Móveis do Azure para Android"
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
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="b2b4f-103">Como usar o SDK de Aplicativos Móveis do Azure para Android</span><span class="sxs-lookup"><span data-stu-id="b2b4f-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="b2b4f-104">Este guia mostra como usar o SDK de cliente Android para Aplicativos Móveis a fim de implementar cenários comuns, como:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="b2b4f-105">Consulta de dados (inserir, atualizar e excluir).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="b2b4f-106">Autenticação.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-106">Authentication.</span></span>
* <span data-ttu-id="b2b4f-107">Tratamento de erros.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-107">Handling errors.</span></span>
* <span data-ttu-id="b2b4f-108">Personalização do cliente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-108">Customizing the client.</span></span>

<span data-ttu-id="b2b4f-109">Este guia destaca o SDK do Android no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="b2b4f-110">Para saber mais sobre os SDKs no servidor para Aplicativos Móveis, confira [Trabalhar com o SDK de back-end do .NET][10] ou [Como usar o SDK de back-end Node.js][11].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="b2b4f-111">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="b2b4f-111">Reference Documentation</span></span>

<span data-ttu-id="b2b4f-112">Você pode encontrar a referência à [API do Javadocs][12] para a biblioteca de cliente Android no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="b2b4f-113">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="b2b4f-113">Supported Platforms</span></span>

<span data-ttu-id="b2b4f-114">O SDK de Aplicativos Móveis do Azure para Android oferece suporte aos níveis de API 19 a 24 (KitKat até Nougat) para fatores de forma de telefone e tablet.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="b2b4f-115">A autenticação, em particular, utiliza uma abordagem comum de estrutura da Web para coletar credenciais.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="b2b4f-116">A autenticação de fluxo do servidor não funciona com dispositivos de fator de forma pequeno como inspeções.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="b2b4f-117">Configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b2b4f-117">Setup and Prerequisites</span></span>

<span data-ttu-id="b2b4f-118">Conclua o tutorial [Início rápido de Aplicativos Móveis](app-service-mobile-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="b2b4f-119">Essa tarefa faz com que todos os pré-requisitos para o desenvolvimento de Aplicativos Móveis do Azure sejam atendidos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="b2b4f-120">O Início Rápido ajuda a configurar sua conta e criar seu primeiro back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="b2b4f-121">Se você decidir não concluir o tutorial de Início Rápido, conclua as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="b2b4f-122">[Criar um back-end do Aplicativo Móvel][13] para usar com seu aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="b2b4f-123">No Android Studio, [atualizar os arquivos de compilação do Gradle](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="b2b4f-124">[Habilitar a permissão de Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="b2b4f-125"><a name="gradle-build"></a>Atualizar o arquivo de compilação do Gradle</span><span class="sxs-lookup"><span data-stu-id="b2b4f-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="b2b4f-126">Altere ambos os arquivos **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="b2b4f-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="b2b4f-127">Adicione este código ao arquivo **build.gradle** do nível *Project* dentro da marca *buildscript*:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="b2b4f-128">Adicione este código ao arquivo **build.gradle** do nível *Module app* dentro da marca *dependencies*:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="b2b4f-129">Atualmente, a versão mais recente é a 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="b2b4f-130">As versões com suporte estão listadas [no bintray][14].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="b2b4f-131"><a name="enable-internet"></a>Habilitar a permissão de Internet</span><span class="sxs-lookup"><span data-stu-id="b2b4f-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="b2b4f-132">Para acessar o Azure, o aplicativo deve ter a permissão INTERNET habilitada.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="b2b4f-133">Se ela ainda não estiver habilitada, adicione a seguinte linha de código ao arquivo **AndroidManifest.xml** :</span><span class="sxs-lookup"><span data-stu-id="b2b4f-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="b2b4f-134">Criar uma conexão de cliente</span><span class="sxs-lookup"><span data-stu-id="b2b4f-134">Create a Client Connection</span></span>

<span data-ttu-id="b2b4f-135">Os Aplicativos Móveis do Azure fornecem quatro funções para seu aplicativo móvel:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="b2b4f-136">Acesso a Dados e a Sincronização Offline com um Serviço de Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="b2b4f-137">Chame as APIs personalizados escritas com o SDK do Servidor de Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="b2b4f-138">Autenticação com autenticação e autorização do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="b2b4f-139">Envie notificações por push com hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="b2b4f-140">Cada uma dessas funções primeiro exige que você crie um objeto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="b2b4f-141">Apenas um objeto `MobileServiceClient` deve ser criado em seu cliente móvel (ou seja, deve ser um padrão Singleton).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="b2b4f-142">Para criar um objeto `MobileServiceClient`:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="b2b4f-143">O `<MobileAppUrl>` é uma cadeia de caracteres ou um objeto de URL que aponta para o back-end móvel.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="b2b4f-144">Se você estiver usando o Serviço de Aplicativo do Azure para hospedar o back-end móvel, use a versão `https://` segura da URL.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="b2b4f-145">O cliente também exige acesso à atividade ou ao contexto - o parâmetro `this` no exemplo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="b2b4f-146">A construção de MobileServiceClient deve acontecer dentro do método `onCreate()` da Atividade referenciada no arquivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="b2b4f-147">Como prática recomendada, você deve abstrair a comunicação do servidor em sua própria classe (padrão singleton).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="b2b4f-148">Nesse caso, você deve passar a Atividade dentro do construtor para configurar corretamente o serviço.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="b2b4f-149">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-149">For example:</span></span>

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

<span data-ttu-id="b2b4f-150">Agora você pode chamar `AzureServiceAdapter.Initialize(this);` no método `onCreate()` de sua atividade principal.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="b2b4f-151">Quaisquer outros métodos que precisam de acesso para o cliente usam `AzureServiceAdapter.getInstance();` para obter uma referência ao adaptador de serviço.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="b2b4f-152">Operações de dados</span><span class="sxs-lookup"><span data-stu-id="b2b4f-152">Data Operations</span></span>

<span data-ttu-id="b2b4f-153">O fundamental do SDK de Aplicativos Móveis do Azure é fornecer acesso aos dados armazenados no SQL Azure no back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="b2b4f-154">Você pode acessar esses dados usando classes fortemente tipadas (preferido) ou consultas não tipadas (não recomendado).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="b2b4f-155">A maior parte desta seção lida com o uso de classes fortemente tipadas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="b2b4f-156">Definir as classes de dados do cliente</span><span class="sxs-lookup"><span data-stu-id="b2b4f-156">Define client data classes</span></span>

<span data-ttu-id="b2b4f-157">Para acessar dados de tabelas do SQL Azure, defina as classes de dados do cliente que correspondem às tabelas no back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="b2b4f-158">Os exemplos deste tópico pressupõem a existência de uma tabela denominada **MyDataTable** com as seguintes colunas:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="b2b4f-159">ID</span><span class="sxs-lookup"><span data-stu-id="b2b4f-159">id</span></span>
* <span data-ttu-id="b2b4f-160">text</span><span class="sxs-lookup"><span data-stu-id="b2b4f-160">text</span></span>
* <span data-ttu-id="b2b4f-161">concluído</span><span class="sxs-lookup"><span data-stu-id="b2b4f-161">complete</span></span>

<span data-ttu-id="b2b4f-162">O objeto tipado do lado do cliente correspondente reside em um arquivo chamado **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="b2b4f-163">Adicione os métodos getter e setter para cada campo que você adicionar.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="b2b4f-164">Se a tabela do SQL Azure contiver mais colunas, adicione os campos correspondentes a essa classe.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="b2b4f-165">Por exemplo, se o DTO (objeto de transferência de dados) tivesse uma coluna Priority de inteiros, você poderia adicionar este campo, com seus métodos getter e setter:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="b2b4f-166">Para saber como criar mais tabelas em seu back-end de Aplicativos Móveis, confira [Como definir um controlador de tabela][15] (back-end do .NET) ou [Como definir tabelas usando um esquema dinâmico ][16] (back-end do Node.js).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="b2b4f-167">Uma tabela de back-end dos Aplicativos Móveis do Azure define cinco campos especiais, quatro deles disponíveis para clientes:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="b2b4f-168">`String id`: A ID globalmente exclusiva para o registro.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="b2b4f-169">Como prática recomendada, torne a ID a representação da Cadeia de caracteres de um objeto [UUID][17].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="b2b4f-170">`DateTimeOffset updatedAt`: a data/hora da última atualização.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="b2b4f-171">O campo updatedAt é definido pelo servidor e nunca deve ser definido pelo código do cliente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="b2b4f-172">`DateTimeOffset createdAt`: a data /hora da criação do objeto.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="b2b4f-173">O campo createdAt é definido pelo servidor e nunca deve ser definido pelo código do cliente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="b2b4f-174">`byte[] version`: normalmente é representado como uma cadeia de caracteres, a versão também é definida pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="b2b4f-175">`boolean deleted`: indica que o registro foi excluído, mas ainda não foi limpo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="b2b4f-176">Não use `deleted` como uma propriedade em sua classe.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="b2b4f-177">O campo `id` é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-177">The `id` field is required.</span></span>  <span data-ttu-id="b2b4f-178">O campo `updatedAt` e o campo `version` são usados para sincronização offline (para sincronização incremental e resolução de conflitos, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="b2b4f-179">O campo `createdAt` é um campo de referência e não é usado pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="b2b4f-180">Os nomes são nomes "across-the-wire" nomes das propriedades e não são ajustáveis.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="b2b4f-181">No entanto, você pode criar um mapeamento entre seu objeto e os nomes "across-the-wire" usando a biblioteca [gson][3].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="b2b4f-182">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-182">For example:</span></span>

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

### <a name="create-a-table-reference"></a><span data-ttu-id="b2b4f-183">Criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="b2b4f-183">Create a Table Reference</span></span>

<span data-ttu-id="b2b4f-184">Para acessar uma tabela, primeiramente crie um objeto [MobileServiceTable][8] chamando o método **getTable** no [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="b2b4f-185">Esse método tem duas sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="b2b4f-186">No código a seguir, **mClient** é uma referência ao objeto MobileServiceClient.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="b2b4f-187">A primeira sobrecarga é usada onde o nome da classe e o nome da tabela são iguais, e é a usada no Início Rápido:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="b2b4f-188">A segunda sobrecarga é usada quando o nome da tabela é diferente do nome da classe: o primeiro parâmetro é o nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="b2b4f-189"><a name="query"></a>Consultar uma tabela de back-end</span><span class="sxs-lookup"><span data-stu-id="b2b4f-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="b2b4f-190">Primeiro, obtenha uma referência de tabela.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-190">First, obtain a table reference.</span></span>  <span data-ttu-id="b2b4f-191">Em seguida, execute uma consulta na referência de tabela.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="b2b4f-192">Uma consulta é qualquer combinação de:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-192">A query is any combination of:</span></span>

* <span data-ttu-id="b2b4f-193">Uma [cláusula de filtro `.where()`](#filtering).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="b2b4f-194">Uma [cláusula de ordenação `.orderBy()`](#sorting).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="b2b4f-195">Uma [cláusula de seleção de campo `.select()`](#selection).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="b2b4f-196">Um `.skip()` e `.top()` para [resultados paginados](#paging).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="b2b4f-197">As cláusulas devem ser apresentadas na ordem anterior.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="b2b4f-198"><a name="filter"></a> Filtragem de resultados</span><span class="sxs-lookup"><span data-stu-id="b2b4f-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="b2b4f-199">A forma geral de uma consulta é:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="b2b4f-200">O exemplo anterior retorna todos os resultados (até o tamanho máximo da página definida pelo servidor).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="b2b4f-201">O método `.execute()` executa a consulta no back-end.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="b2b4f-202">A consulta é convertida em uma consulta [OData v3][19] antes da transmissão para o back-end de Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="b2b4f-203">Após o recebimento, o back-end dos Aplicativos Móveis converte a consulta em uma instrução SQL antes de executá-la na instância do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="b2b4f-204">Como a atividade de rede demora algum tempo, o método `.execute()` retorna um [`ListenableFuture<E>`][18].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="b2b4f-205"><a name="filtering"></a>Filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="b2b4f-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="b2b4f-206">A execução da consulta a seguir retorna todos os itens da tabela **ToDoItem**, em que **complete** é igual a **false**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-207">**mToDoTable** é a referência à tabela do serviço móvel que criamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="b2b4f-208">Defina um filtro usando a chamada ao método **where** na referência de tabela.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="b2b4f-209">O método **where** é seguido de um método **field** seguido de um método que especifica o predicado lógico.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="b2b4f-210">Os possíveis métodos de predicado incluem **eq** (igual),**ne** (diferente), **gt** (maior que), **ge** (maior que ou igual a), **lt** (menor que), **le** (menor que ou igual a).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="b2b4f-211">Esses métodos permitem que você compare os campos de número e cadeia de caracteres com valores específicos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="b2b4f-212">Você pode filtrar por datas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-212">You can filter on dates.</span></span> <span data-ttu-id="b2b4f-213">Os métodos a seguir permitem comparar o campo de data inteira ou partes da data:**year**, **month**, **day**, **hour**, **minute** e **second**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="b2b4f-214">O exemplo a seguir adiciona um filtro para itens cuja *data de vencimento* é igual a 2013.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-215">Os métodos a seguir oferecem suporte a filtros complexos nos campos de cadeia de caracteres: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim** e **length**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="b2b4f-216">O exemplo a seguir filtra linhas de tabela em que a coluna *text* começa com "PRI0".</span><span class="sxs-lookup"><span data-stu-id="b2b4f-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-217">Os métodos de operador a seguir têm suporte em campos de número: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling** e **round**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="b2b4f-218">O exemplo a seguir filtra linhas de tabela em que **duration** é um número par.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-219">É possível combinar predicados com estes métodos lógicos: **and**, **or** e **not**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="b2b4f-220">O exemplo a seguir combina dois dos exemplos anteriores.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-221">Agrupar e aninhar operadores lógicos:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-221">Group and nest logical operators:</span></span>

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

<span data-ttu-id="b2b4f-222">Para ver uma discussão mais detalhada e exemplos de filtragem, veja [Explorar a riqueza do modelo de consulta de cliente do Android][20].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="b2b4f-223"><a name="sorting"></a>Classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="b2b4f-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="b2b4f-224">O código a seguir retorna todos os itens de uma tabela **ToDoItem** classificada em ordem crescente pelo campo *text* .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="b2b4f-225">*mToDoTable* é a referência à tabela de back-end criada anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-226">O primeiro parâmetro do método **orderBy** é uma cadeia de caracteres igual ao nome do campo pelo qual classificar.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="b2b4f-227">O segundo parâmetro usa a enumeração **QueryOrder** para especificar se a classificação será feita em ordem crescente ou decrescente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="b2b4f-228">Se você estiver filtrando usando o método ***where***, o método ***where*** deverá ser invocado antes do método ***orderBy***.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="b2b4f-229"><a name="selection"></a>Selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="b2b4f-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="b2b4f-230">O código a seguir ilustra como retornar todos os itens de uma tabela de **ToDoItems**, mas exibe apenas os **complete** e **text**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="b2b4f-231">**mToDoTable** é a referência à tabela de back-end criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-232">Os parâmetros para a função select são os nomes de cadeia de caracteres das colunas da tabela que você deseja retornar.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="b2b4f-233">O método **select** precisa seguir métodos como **where** e **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="b2b4f-234">Ele pode ser seguido por métodos de paginação como **skip** e **top**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="b2b4f-235"><a name="paging"></a>Retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="b2b4f-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="b2b4f-236">Os dados **SEMPRE** retornam em páginas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="b2b4f-237">O número máximo de registros retornados é definido pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="b2b4f-238">Se o cliente solicitar mais registros, o servidor retornará o número máximo de registros.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="b2b4f-239">Por padrão, o tamanho máximo da página no servidor é de 50 registros.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="b2b4f-240">O primeiro exemplo mostra como selecionar os cinco primeiros itens de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="b2b4f-241">A consulta retorna os itens de uma tabela **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="b2b4f-242">**mToDoTable** é a referência à tabela de back-end criada anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-243">Veja uma consulta que ignora os cinco primeiros itens e retorna os cinco seguintes:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="b2b4f-244">Se você quiser obter todos os registros em uma tabela, implemente o código para iterar por todas as páginas:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

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

<span data-ttu-id="b2b4f-245">Uma solicitação para todos os registros usando esse método cria no mínimo duas solicitações para o back-end dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="b2b4f-246">A escolha do tamanho de página certo é um equilíbrio entre o uso de memória durante a solicitação, o uso de largura de banda e atraso no recebimento completo dos dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="b2b4f-247">O padrão (50 registros) é adequado para todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="b2b4f-248">Se você operar exclusivamente em dispositivos de memória maiores, aumente até 500.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="b2b4f-249">Descobrimos que aumentar o tamanho da página além dos 500 registros resulta em atrasos inaceitáveis e problemas de memória grande.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="b2b4f-250"><a name="chaining"></a>Como concatenar métodos de consulta</span><span class="sxs-lookup"><span data-stu-id="b2b4f-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="b2b4f-251">Os métodos usados nas tabelas de back-end de consulta podem ser concatenados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="b2b4f-252">O encadeamento de métodos de consulta permite a você selecionar colunas específicas ou linhas filtradas que são classificadas e paginadas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="b2b4f-253">Você pode criar filtros lógicos complexos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-253">You can create complex logical filters.</span></span>  <span data-ttu-id="b2b4f-254">Cada método de consulta retorna um objeto de consulta.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-254">Each query method returns a Query object.</span></span> <span data-ttu-id="b2b4f-255">Para encerrar a série de métodos e realmente executar a consulta, chame o método **execute** .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="b2b4f-256">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-256">For example:</span></span>

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

<span data-ttu-id="b2b4f-257">Os métodos de consulta encadeados devem ser ordenados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="b2b4f-258">Métodos de filtragem (**where**).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="b2b4f-259">Métodos de classificação (**orderBy**).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="b2b4f-260">Métodos de seleção (**select**).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="b2b4f-261">Métodos de paginação (**skip** e **top**).</span><span class="sxs-lookup"><span data-stu-id="b2b4f-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="b2b4f-262"><a name="binding"></a>Associar dados à interface do usuário</span><span class="sxs-lookup"><span data-stu-id="b2b4f-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="b2b4f-263">A associação de dados envolve três componentes:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-263">Data binding involves three components:</span></span>

* <span data-ttu-id="b2b4f-264">A fonte de dados</span><span class="sxs-lookup"><span data-stu-id="b2b4f-264">The data source</span></span>
* <span data-ttu-id="b2b4f-265">O layout da tela</span><span class="sxs-lookup"><span data-stu-id="b2b4f-265">The screen layout</span></span>
* <span data-ttu-id="b2b4f-266">O adaptador que vincula os dois.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="b2b4f-267">Em nosso código de exemplo, retornamos os dados da tabela **ToDoItem** do SQL Azure dos Aplicativos Móveis em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="b2b4f-268">Essa atividade é um padrão comum para aplicativos de dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="b2b4f-269">As consultas de banco de dados geralmente retornam uma coleção de linhas que o cliente obtém em uma lista ou uma matriz.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="b2b4f-270">Neste exemplo, a matriz é a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="b2b4f-271">O código especifica um layout de tela que define a exibição dos dados que são exibidos no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="b2b4f-272">E os dois são associados juntos com um adaptador, que, nesse código, é uma extensão da classe **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="b2b4f-273"><a name="layout"></a>Definir o layout</span><span class="sxs-lookup"><span data-stu-id="b2b4f-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="b2b4f-274">O layout é definido por vários trechos de código XML.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="b2b4f-275">Com base em um layout existente, o código a seguir representa a **ListView** que queremos preencher com nossos dados de servidor.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="b2b4f-276">No código anterior, o atributo *listitem* especifica a id do layout para uma linha individual na lista.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="b2b4f-277">Esse código especifica uma caixa de seleção e seu texto associado, e tem uma instância criada para cada item na lista.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="b2b4f-278">Esse layout não exibe o campo **ID** , e um layout mais complexo especificaria campos adicionais na exibição.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="b2b4f-279">Este código está no arquivo **row_list_to_do.xml**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-279">This code is in the **row_list_to_do.xml** file.</span></span>

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

#### <span data-ttu-id="b2b4f-280"><a name="adapter"></a>Definir o adaptador</span><span class="sxs-lookup"><span data-stu-id="b2b4f-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="b2b4f-281">Como a fonte de dados da nossa exibição é uma matriz de**ToDoItem**, podemos criar a subclasse do nosso adaptador por meio de uma classe **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="b2b4f-282">Esta subclasse produz uma exibição para cada **ToDoItem** usando o layout **row_list_to_do**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="b2b4f-283">No nosso código, definimos a seguinte classe que é uma extensão da classe **ArrayAdapter&lt;E&gt;**:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="b2b4f-284">Substitua o método **getView** dos adaptadores.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="b2b4f-285">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-285">For example:</span></span>

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

<span data-ttu-id="b2b4f-286">Criamos uma instância dessa classe em nossa atividade, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="b2b4f-287">O segundo parâmetro para o construtor ToDoItemAdapter é uma referência ao layout.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="b2b4f-288">Agora podemos criar uma instância do **ListView** e atribuir o adaptador ao **ListView**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="b2b4f-289"><a name="use-adapter"></a>Usar o Adaptador para associar-se à interface do usuário</span><span class="sxs-lookup"><span data-stu-id="b2b4f-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="b2b4f-290">Agora você está pronto para usar a associação de dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-290">You are now ready to use data binding.</span></span> <span data-ttu-id="b2b4f-291">O código a seguir mostra como obter os itens na tabela e preenche o adaptador local com os itens retornados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

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

<span data-ttu-id="b2b4f-292">Chame o adaptador sempre que modificar a tabela **ToDoItem** .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="b2b4f-293">Como as modificações são feitas de registro em registro, você trata de uma única linha em vez de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="b2b4f-294">Ao inserir um item, chame o método **add** no adaptador e, ao excluir, chame o método **remove**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="b2b4f-295">Encontre um exemplo completo no [Projeto de Início Rápido do Android][21].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="b2b4f-296"><a name="inserting"></a>Inserir dados no back-end</span><span class="sxs-lookup"><span data-stu-id="b2b4f-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="b2b4f-297">Crie uma instância da classe *ToDoItem* e defina suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="b2b4f-298">Em seguida, use **insert ()** para inserir um objeto:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="b2b4f-299">A entidade retornada corresponde aos dados inseridos na tabela de back-end, inclusive a ID e outros valores (como os campos `createdAt`, `updatedAt` e `version`) definidos no back-end.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="b2b4f-300">As tabelas de Aplicativos Móveis exigem uma coluna de chave primária denominada **id**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="b2b4f-301">Essa coluna deve ser uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-301">This column must be a string.</span></span> <span data-ttu-id="b2b4f-302">O valor padrão da coluna de ID é um GUID.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="b2b4f-303">Você pode fornecer outros valores exclusivos, como endereços de email ou nomes de usuário.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="b2b4f-304">Quando um valor de ID de cadeia de caracteres não é fornecido para um registro inserido, o back-end gera um novo GUID.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="b2b4f-305">Os valores de ID de cadeia de caracteres proporcionam as seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="b2b4f-306">As IDs podem ser geradas sem que seja preciso fazer uma varredura no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="b2b4f-307">Os registros são mais fáceis de mesclar a partir de tabelas ou bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="b2b4f-308">Os valores de ID integram-se melhor à lógica de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="b2b4f-309">Valores de ID de cadeia de caracteres são **OBRIGATÓRIOS** para suporte de sincronização offline.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="b2b4f-310">Você não pode alterar uma ID após ela ser armazenada no banco de dados back-end.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="b2b4f-311"><a name="updating"></a>Atualizar dados em um aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="b2b4f-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="b2b4f-312">Para atualizar dados em uma tabela, passe o novo objeto para o método **update ()** .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="b2b4f-313">Neste exemplo, *item* é uma referência a uma linha na tabela *ToDoItem*, a qual sofreu algumas alterações.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="b2b4f-314">A linha com a mesma **id** é atualizada.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="b2b4f-315"><a name="deleting"></a>Excluir dados em um aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="b2b4f-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="b2b4f-316">O código a seguir mostra como excluir dados de uma tabela especificando o objeto de dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="b2b4f-317">Você também pode excluir um item especificando a **id** da linha a ser excluída.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="b2b4f-318"><a name="lookup"></a>Pesquisar um item específico por ID</span><span class="sxs-lookup"><span data-stu-id="b2b4f-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="b2b4f-319">Pesquise um item com determinado campo **id** com o método **lookUp()**:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="b2b4f-320"><a name="untyped"></a>Como trabalhar com dados não tipados</span><span class="sxs-lookup"><span data-stu-id="b2b4f-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="b2b4f-321">O modelo de programação não tipado oferece controle rígido sobre a serialização JSON.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="b2b4f-322">Há alguns cenários comuns em que você pode querer usar um modelo de programação não tipado.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="b2b4f-323">Por exemplo, se sua tabela de back-end contém muitas colunas e você só precisa fazer referência a um subconjunto das colunas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="b2b4f-324">O modelo tipado requer que você defina todas as colunas definidas no back-end dos Aplicativos Móveis em sua classe de dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="b2b4f-325">A maioria das chamadas API para acessar dados são semelhante às chamadas de programação tipadas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="b2b4f-326">A principal diferença é que o modelo não tipado você invocar métodos no objeto **MobileServiceJsonTable**, em vez do objeto **MobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="b2b4f-327"><a name="json_instance"></a>Criar uma instância de uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="b2b4f-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="b2b4f-328">Semelhante ao modelo tipado, você começa obtendo uma referência de tabela, mas, nesse caso, é um objeto **MobileServicesJsonTable** .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="b2b4f-329">Obtenha a referência ao chamar o método **getTable** em uma instância do cliente:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="b2b4f-330">Depois de criar uma instância do **MobileServiceJsonTable**, ela tem praticamente a mesma API disponível que o modelo de programação tipado.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="b2b4f-331">Em alguns casos, os métodos usam um parâmetro não tipado em vez de um parâmetro tipado.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="b2b4f-332"><a name="json_insert"></a>Inserir em uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="b2b4f-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="b2b4f-333">O código a seguir mostra como fazer uma inserção.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="b2b4f-334">A primeira etapa consiste em criar um [JsonObject][1], que faz parte da biblioteca [gson][3].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="b2b4f-335">Em seguida, use **insert()** para inserir o objeto não tipado na tabela.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="b2b4f-336">Se você precisa obter a ID do objeto inserido, use o método **getAsJsonPrimitive()** .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="b2b4f-337"><a name="json_delete"></a>Excluir de uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="b2b4f-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="b2b4f-338">O código a seguir mostra como excluir uma instância, neste caso, a mesma instância de um **JsonObject** criado no exemplo *insert* anterior.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="b2b4f-339">O código é igual ao do caso tipado, mas o método tem uma assinatura diferente, uma vez que ele faz referência a um **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="b2b4f-340">Você também pode excluir uma instância diretamente, usando sua ID:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="b2b4f-341"><a name="json_get"></a>Retornar todas as linhas de uma tabela não tipada</span><span class="sxs-lookup"><span data-stu-id="b2b4f-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="b2b4f-342">O código a seguir mostra como recuperar uma tabela inteira.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="b2b4f-343">Como você está usando uma tabela JSON, pode recuperar seletivamente somente algumas das colunas da tabela.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

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

<span data-ttu-id="b2b4f-344">O mesmo conjunto de métodos de filtragem, filtragem e paginação que estão disponíveis para o modelo tipado estão disponíveis para o modelo não tipado.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="b2b4f-345"><a name="offline-sync"></a>Implementar a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="b2b4f-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="b2b4f-346">O SDK do cliente de Aplicativos Móveis do Azure também implementa a sincronização offline de dados usando um banco de dados SQLite para armazenar localmente uma cópia dos dados do servidor.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="b2b4f-347">As operações executadas em uma tabela offline não exigem conectividade móvel para funcionar.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="b2b4f-348">A sincronização offline auxilia na resiliência e no desempenho às custas de uma lógica mais complexa para resolução de conflitos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="b2b4f-349">O SDK de cliente dos Aplicativos Móveis do Azure implementa os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="b2b4f-350">Sincronização Incremental: somente registros novos e atualizados são baixados, economizando o consumo de largura de banda e de memória.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="b2b4f-351">Simultaneidade Otimista: pressupõe-se que as operações terão êxito.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="b2b4f-352">A resolução de conflitos é adiada até que as atualizações sejam executadas no servidor.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="b2b4f-353">Resolução de Conflitos: o SDK detecta quando uma alteração conflitante tiver sido feita no servidor e fornece ganchos para alertar o usuário.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="b2b4f-354">Exclusão Reversível: os registros excluídos são marcadas como excluídos, permitindo que outros dispositivos atualizem seu cache offline.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="b2b4f-355">Inicializar a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="b2b4f-355">Initialize Offline Sync</span></span>

<span data-ttu-id="b2b4f-356">Cada tabela offline deve ser definida no cache offline antes do uso.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="b2b4f-357">Normalmente, a definição da tabela é feita imediatamente após a criação do cliente:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-357">Normally, table definition is done immediately after the creation of the client:</span></span>

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

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
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

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="b2b4f-358">Obter uma referência à Tabela de Cache Offline</span><span class="sxs-lookup"><span data-stu-id="b2b4f-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="b2b4f-359">Para uma tabela online, use `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="b2b4f-360">Para uma tabela offline, use `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="b2b4f-361">Todos os métodos disponíveis para tabelas online (incluindo a filtragem, classificação, paginação, inserção de dados, atualização de dados e exclusão de dados) funcionam igualmente bem em tabelas online e offline.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="b2b4f-362">Sincronizar o Cache Offline Local</span><span class="sxs-lookup"><span data-stu-id="b2b4f-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="b2b4f-363">A sincronização está dentro do controle de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="b2b4f-364">Veja um exemplo de método de sincronização:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-364">Here is an example synchronization method:</span></span>

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

<span data-ttu-id="b2b4f-365">Se um nome de consulta for fornecido para o método `.pull(query, queryname)`, a sincronização incremental será usada para retornar somente os registros criados ou alterados desde o último pull concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="b2b4f-366">Lidar com conflitos durante a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="b2b4f-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="b2b4f-367">Se um conflito ocorrer durante uma operação `.push()`, uma `MobileServiceConflictException` será lançada.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="b2b4f-368">O item emitido pelo servidor é inserido na exceção e pode ser recuperado por `.getItem()` na exceção.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="b2b4f-369">Ajuste o envio por push chamando os seguintes itens no objeto MobileServiceSyncContext:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="b2b4f-370">Depois que todos os conflitos forem marcados conforme sua vontade, chame `.push()` novamente para resolver todos os conflitos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="b2b4f-371"><a name="custom-api"></a>Chamar uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="b2b4f-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="b2b4f-372">Uma API personalizada permite que você defina pontos de extremidade personalizados que expõem a funcionalidade do servidor que não mapeia para uma inserção, atualização, exclusão ou operação de leitura.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="b2b4f-373">Usando uma API personalizada, você pode ter mais controle sobre mensagens, incluindo ler e definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem diferente do JSON.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="b2b4f-374">Em um cliente Android, você chama o método **invokeApi** para chamar o ponto de extremidade da API personalizada.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="b2b4f-375">O exemplo a seguir mostra como chamar um ponto de extremidade de API denominado **completeAll**, que retorna uma classe de coleção chamada **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

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

<span data-ttu-id="b2b4f-376">O método **invokeApi** é chamado no cliente, que envia uma solicitação POST para a nova API personalizada.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="b2b4f-377">O resultado retornado pela API personalizada é exibido em uma caixa de diálogo de mensagem, se houver erros.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="b2b4f-378">Outras versões de **invokeApi** permitem que você, opcionalmente, envie um objeto no corpo da solicitação, especifique o método HTTP e envie parâmetros de consulta com a solicitação.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="b2b4f-379">Versões não tipadas de **invokeApi** também são fornecidas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="b2b4f-380"><a name="authentication"></a>Adicionar autenticação ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b2b4f-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="b2b4f-381">Os tutoriais já descrevem detalhadamente como adicionar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="b2b4f-382">O Serviço de Aplicativo oferece suporte à [autenticação de usuários do aplicativo](app-service-mobile-android-get-started-users.md) usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft, Twitter e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="b2b4f-383">Você pode definir permissões em tabelas para restringir o acesso a operações específicas apenas para usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="b2b4f-384">Você também pode usar a identidade de usuários autenticados para implementar regras de autorização no seu back-end.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="b2b4f-385">Dois fluxos de autenticação são suportados: um **server** flow e um **client** flow.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="b2b4f-386">O fluxo de servidor fornece a experiência de autenticação mais simples, pois depende da interface Web do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="b2b4f-387">Nenhum SDK adicional é necessário para implementar a autenticação de fluxo de servidor.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="b2b4f-388">A autenticação de fluxo de servidor não oferece uma integração profunda ao dispositivo móvel e só é recomendada em cenários de prova de conceito.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="b2b4f-389">O fluxo de cliente permite uma integração mais profunda com funcionalidades específicas do dispositivo, como logon único, uma vez que depende de SDKs fornecidas pelo provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="b2b4f-390">Por exemplo, você pode integrar o SDK do Facebook a seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="b2b4f-391">O cliente móvel alterna para o aplicativo do Facebook e confirma o logon antes de voltar para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="b2b4f-392">Quatro etapas são necessárias para habilitar a autenticação no seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="b2b4f-393">Registrar o aplicativo para autenticação com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="b2b4f-394">Configurar o back-end do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="b2b4f-395">Restringir permissões de tabela a usuários autenticados somente no back-end do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="b2b4f-396">Adicionar código de autenticação ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-396">Add authentication code to your app.</span></span>

<span data-ttu-id="b2b4f-397">Você pode definir permissões em tabelas para restringir o acesso a operações específicas apenas para usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="b2b4f-398">Você também pode usar o SID de um usuário autenticado para modificar solicitações.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="b2b4f-399">Para saber mais, confira [Introdução à autenticação] e a documentação TUTORIAL do SDK do Servidor.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="b2b4f-400"><a name="caching"></a>Autenticação: Fluxo de servidor</span><span class="sxs-lookup"><span data-stu-id="b2b4f-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="b2b4f-401">O código a seguir inicia um processo de logon do fluxo do servidor usando o provedor Google.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="b2b4f-402">A configuração adicional é necessária devido aos requisitos de segurança para o provedor do Google:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="b2b4f-403">Além disso, adicione o método a seguir à classe Activity:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="b2b4f-404">O `GOOGLE_LOGIN_REQUEST_CODE` definidos em sua Atividade principal é usado para o método `login()` e dentro do método `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="b2b4f-405">Você pode escolher qualquer número exclusivo, desde que o mesmo número seja usado dentro do método `login()` e do método `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="b2b4f-406">Se você abstrair o código do cliente em um adaptador de serviço (conforme mostrado anteriormente), chame os métodos apropriados no adaptador de serviço.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="b2b4f-407">Você também precisa configurar o projeto para customtabs.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="b2b4f-408">Primeiro, especifique uma URL de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="b2b4f-409">Adicione este trecho ao `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

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

<span data-ttu-id="b2b4f-410">Adicione o **redirectUriScheme** ao arquivo `build.gradle` de seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

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

<span data-ttu-id="b2b4f-411">Finalmente, adicione `com.android.support:customtabs:23.0.1` à lista de dependências no arquivo `build.gradle`:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

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

<span data-ttu-id="b2b4f-412">Obtenha a ID do usuário conectado de um **MobileServiceUser** usando o método **getUserId**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="b2b4f-413">Para ver um exemplo de como usar Futures para chamar as APIs de logon assíncronas, veja [Introdução à autenticação].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="b2b4f-414">O esquema de URL mencionado diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="b2b4f-415">Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` tenham as mesmas maiúsculas ou minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="b2b4f-416"><a name="caching"></a>Armazenar tokens de autenticação em cache</span><span class="sxs-lookup"><span data-stu-id="b2b4f-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="b2b4f-417">Armazenar em cache os tokens de autenticação exige que você armazene uma ID de usuário e o token de autenticação localmente no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="b2b4f-418">Na próxima vez que o aplicativo iniciar, você verificará o cache e, se esses valores estiverem presentes, poderá ignorar o procedimento de logon e reidratar o cliente com esses dados.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="b2b4f-419">No entanto, esses dados são confidenciais e, para segurança, devem ser armazenados criptografados caso o telefone seja roubado.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="b2b4f-420">Veja um exemplo completo de como armazenar em cache os tokens de autenticação na [seção Armazenar em cache os tokens de autenticação][7].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="b2b4f-421">Ao tentar usar um token expirado, você receberá uma resposta *401 não autorizado* .</span><span class="sxs-lookup"><span data-stu-id="b2b4f-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="b2b4f-422">Você pode tratar erros de autenticação usando filtros.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="b2b4f-423">Filtros interceptam as solicitações para o back-end do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="b2b4f-424">O código do filtro testa a resposta para um 401, dispara o processo de logon e retoma a solicitação que gerou o 401.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="b2b4f-425"><a name="refresh"></a>Usar tokens de atualização</span><span class="sxs-lookup"><span data-stu-id="b2b4f-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="b2b4f-426">O token retornado pela Autenticação e Autorização do Serviço de Aplicativo do Azure tem um tempo de vida definido de uma hora.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="b2b4f-427">Após esse período, você deve autenticar novamente o usuário.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="b2b4f-428">Se você estiver usando um token de vida longa recebido por meio da autenticação de fluxo de cliente, autentique novamente com a Autenticação e Autorização do Serviço de Aplicativo do Azure usando o mesmo token.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="b2b4f-429">Outro token de Serviço de Aplicativo do Azure é gerado com um novo tempo de vida.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="b2b4f-430">Você também pode registrar o provedor para usar Tokens de atualização.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="b2b4f-431">Nem sempre um token de atualização está disponível.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="b2b4f-432">É necessário realizar uma configuração adicional:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-432">Additional configuration is required:</span></span>

* <span data-ttu-id="b2b4f-433">Para o **Azure Active Directory**, configure um segredo do cliente para o aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="b2b4f-434">Especifique o segredo do cliente no Serviço de Aplicativo do Azure ao configurar a Autenticação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="b2b4f-435">Ao chamar `.login()`, passe `response_type=code id_token` como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="b2b4f-436">Para o **Google**, passe o `access_type=offline` como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="b2b4f-437">Para a **Conta da Microsoft**, selecione o escopo `wl.offline_access`.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="b2b4f-438">Para atualizar um token, chame `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="b2b4f-439">Como prática recomendada, crie um filtro que detecta uma resposta 401 do servidor e tenta atualizar o token de usuário.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="b2b4f-440">Faça logon com a autenticação de cliente-fluxo</span><span class="sxs-lookup"><span data-stu-id="b2b4f-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="b2b4f-441">O processo geral para fazer logon com autenticação de cliente-fluxo é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="b2b4f-442">Configure a Autenticação e Autorização do Serviço de Aplicativo do Azure como você faria com autenticação de servidor-fluxo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="b2b4f-443">Integre o SDK do provedor para autenticação para produzir um token de acesso do.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="b2b4f-444">Chame o método `.login()` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-444">Call the `.login()` method as follows:</span></span>

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

<span data-ttu-id="b2b4f-445">Substitua o método `onSuccess()` por qualquer código que você queira usar em um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="b2b4f-446">A cadeia de caracteres `{provider}` é um provedor válido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount** ou **twitter**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="b2b4f-447">Se você tiver implementado a autenticação personalizada, também poderá usar a marca do provedor de autenticação personalizada.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="b2b4f-448"><a name="adal"></a>Autenticar usuários com a Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="b2b4f-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="b2b4f-449">Você pode usar a ADAL (Biblioteca de autenticação do Active Directory) para conectar os usuários ao seu aplicativo usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="b2b4f-450">Normalmente, é melhor usar um logon de fluxo de cliente em vez dos métodos `loginAsync()` , pois ele fornece uma aparência mais nativa de UX e permite uma maior personalização.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="b2b4f-451">Configure o seu back-end de aplicativo móvel para entrada no AAD seguindo o tutorial [Como configurar o Serviço de Aplicativo para logon no Active Directory][22].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="b2b4f-452">Complete a etapa opcional de registrar um aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="b2b4f-453">Instale a ADAL modificando o arquivo build.gradle para incluir as seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

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

1. <span data-ttu-id="b2b4f-454">Adicione o seguinte código ao seu aplicativo, fazendo as seguintes substituições:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="b2b4f-455">Substitua **INSERT-AUTHORITY-HERE** pelo nome do locatário no qual o aplicativo foi provisionado.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="b2b4f-456">O formato deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="b2b4f-457">Substitua **INSERT-RESOURCE-ID-HERE** pela ID do cliente do seu back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="b2b4f-458">Você pode obter a ID do cliente na guia **Avançadas** em **Configurações do Azure Active Directory** no portal.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="b2b4f-459">Substitua **INSERT-CLIENT-ID-HERE** pela ID do cliente copiada do aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="b2b4f-460">Substitua **INSERT-REDIRECT-URI-HERE** pelo ponto de extremidade */.auth/login/done* do site, usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="b2b4f-461">Esse valor deve ser similar a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <span data-ttu-id="b2b4f-462"><a name="filters"></a>Ajustar a comunicação cliente-servidor</span><span class="sxs-lookup"><span data-stu-id="b2b4f-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="b2b4f-463">A conexão do cliente é normalmente uma conexão HTTP básica usando a biblioteca HTTP subjacente fornecida com o SDK do Android.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="b2b4f-464">Há vários motivos para você querer alterar isso:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="b2b4f-465">Você quer usar uma biblioteca HTTP alternativa para ajustar o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="b2b4f-466">Você quer fornecer uma barra de progresso.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="b2b4f-467">Você quer adicionar um cabeçalho personalizado para oferecer suporte à funcionalidade de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="b2b4f-468">Você quer interceptar uma resposta com falha para que você possa implementar a reautenticação.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="b2b4f-469">Você quer registrar solicitações de back-end para um serviço de análise.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="b2b4f-470">Usar uma biblioteca HTTP alternativa</span><span class="sxs-lookup"><span data-stu-id="b2b4f-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="b2b4f-471">Chame o método `.setAndroidHttpClientFactory()` imediatamente depois de criar sua referência de cliente.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="b2b4f-472">Por exemplo, para definir o tempo limite de conexão como 60 segundos (em vez do padrão de 10 segundos):</span><span class="sxs-lookup"><span data-stu-id="b2b4f-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

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

### <a name="implement-a-progress-filter"></a><span data-ttu-id="b2b4f-473">Implementar um filtro de progresso</span><span class="sxs-lookup"><span data-stu-id="b2b4f-473">Implement a Progress Filter</span></span>

<span data-ttu-id="b2b4f-474">Você pode implementar uma interceptação de cada solicitação implementando um `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="b2b4f-475">Por exemplo, o seguinte atualiza uma barra de progresso pré-criada:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-475">For example, the following updates a pre-created progress bar:</span></span>

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

<span data-ttu-id="b2b4f-476">Você pode anexar esse filtro ao cliente da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="b2b4f-477">Personalizar cabeçalhos de solicitações</span><span class="sxs-lookup"><span data-stu-id="b2b4f-477">Customize Request Headers</span></span>

<span data-ttu-id="b2b4f-478">Use o seguinte `ServiceFilter` e anexe o filtro da mesma maneira que o `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="b2b4f-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

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

### <span data-ttu-id="b2b4f-479"><a name="conversions"></a>Configurar a Serialização Automática</span><span class="sxs-lookup"><span data-stu-id="b2b4f-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="b2b4f-480">Você pode especificar uma estratégia de conversão que se aplica a todas as colunas usando a API [gson][3].</span><span class="sxs-lookup"><span data-stu-id="b2b4f-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="b2b4f-481">A biblioteca do cliente Android usa [gson][3] nos bastidores para serializar objetos Java para dados JSON antes que os dados sejam são enviados aos Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="b2b4f-482">O código a seguir usa o método **setFieldNamingStrategy ()** para definir a estratégia.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="b2b4f-483">Esse exemplo excluirá o caractere inicial (um "m") e, em seguida, a minúscula do próximo caractere, para cada nome de campo.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="b2b4f-484">Por exemplo, ele poderia transformar "mId" em "id".</span><span class="sxs-lookup"><span data-stu-id="b2b4f-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="b2b4f-485">Implementar uma estratégia de conversão para reduzir a necessidade de anotações `SerializedName()` na maioria dos campos.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

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

<span data-ttu-id="b2b4f-486">Esse código deve ser executado antes da criação de uma referência de cliente móvel usando o **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="b2b4f-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="b2b4f-487">[Introdução à autenticação]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="b2b4f-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
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
