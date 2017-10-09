---
title: "aaaAzure AD v2 Android Introdução - instalação | Microsoft Docs"
description: Como um aplicativo do Android pode obter um token de acesso e chamar a API do Microsoft Graph ou APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurar o seu projeto

> Preferir toodownload Android Studio projeto desse exemplo em vez disso? [Baixar um projeto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.


### <a name="create-a-new-project"></a>Criar um novo projeto 
1.  Abra o Android Studio e acesse: `File` > `New` > `New Project`
2.  Nomeie o aplicativo e clique em `Next`
3.  Certifique-se de que tooselect *21 de API ou mais recente (Android 5.0)* e clique em`Next`
4.  Mantenha `Empty Activity`, clique em `Next` e, em seguida, em `Finish`


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Adicionar projeto de tooyour Olá biblioteca de autenticação da Microsoft (MSAL)
1.  No Android Studio, acesse: `Gradle Scripts` > `build.gradle (Module: app)`
2.  Copiar e colar a seguir Olá código em `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>Sobre este pacote

pacote de saudação acima instala Olá biblioteca de autenticação da Microsoft (MSAL). MSAL lida com a aquisição, cache e atualizar usuário tokens usados tooaccess APIs protegidos pelo ponto de extremidade do Active Directory do Azure v2.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>Criar a interface do usuário do aplicativo

1.  Abra `activity_main.xml` em `res` > `layout`
2.  Alterar o layout de atividade de saudação do `android.support.constraint.ConstraintLayout` ou outros muito`LinearLayout`
3.  Adicionar `android:orientation="vertical"` propriedade muito`LinearLayout` nó
4.  Copiar e colar a seguir Olá código em Olá `LinearLayout` nó, substituindo o conteúdo atual da saudação:

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

