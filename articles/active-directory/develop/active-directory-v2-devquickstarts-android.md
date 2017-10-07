---
title: aplicativo do Android aaaAzure do Active Directory v 2.0 | Microsoft Docs
description: "Como um aplicativo do Android que conecta os usuários com pessoais conta da Microsoft e trabalho ou escolares e chamadas de toobuild Olá API do Graph usando bibliotecas de terceiros."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Adicionar aplicativo do Android tooan entrar usando uma biblioteca de terceiros com a API do Graph usando o ponto de extremidade do hello v 2.0
plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect. Os desenvolvedores podem usar qualquer biblioteca quiserem toointegrate com nossos serviços. os desenvolvedores de toohelp usar nossa plataforma com outras bibliotecas, escrevemos algumas instruções passo a passo como esse um toodemonstrate como plataforma de identidade da Microsoft tooconnect toohello tooconfigure bibliotecas de terceiros. A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) pode se conectar a plataforma de identidade do Microsoft toohello.

Com o aplicativo hello que cria este passo a passo, os usuários podem entrar na organização tootheir e pesquisar por si mesmos em sua organização usando Olá API do Graph.

Se você for novo tooOAuth2 ou OpenID Connect, muito dessa configuração de exemplo pode não fazer sentido tooyou. É recomendável ler o artigo [Protocolos 2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md) para obter mais informações.

> [!NOTE]
> Alguns recursos de nossa plataforma que têm uma expressão em Olá OAuth2 ou padrões de OpenID Connect, como acesso condicional e gerenciamento de política do Intune, exigem você toouse nosso código-fonte aberto bibliotecas de identidade do Microsoft Azure.
> 
> 

o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure.

> [!NOTE]
> toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Baixar o código de saudação do GitHub
código de saudação para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) ou esqueleto de saudação do clone:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

Você também pode baixar o exemplo hello e começar imediatamente:

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>Registrar um aplicativo
Criar um novo aplicativo no hello [portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga Olá etapas detalhadas em [como tooregister um aplicativo com o ponto de extremidade do hello v 2.0](active-directory-v2-app-registration.md).  Não se esqueça de:

* Saudação de cópia **Id do aplicativo** que é atribuído tooyour aplicativo porque você precisará dele em breve.
* Adicionar Olá **Mobile** plataforma para seu aplicativo.

> Observação: o portal de registro de aplicativo hello fornece um **URI de redirecionamento** valor. No entanto, neste exemplo você deve usar o valor padrão Olá `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Baixar a biblioteca de terceiros NXOAuth2 hello e criar um espaço de trabalho
Para este passo a passo, você usará Olá OIDCAndroidLib do GitHub, que é uma biblioteca de OAuth2 com base em Olá código OpenID Connect do Google. Ele implementa um perfil de aplicativo nativo hello e dá suporte ao ponto de extremidade de autorização de saudação do usuário hello. Essas são todas as coisas hello, você precisará toointegrate com a plataforma de identidade Microsoft hello.

Clone um computador de tooyour Olá OIDCAndroidLib repositório.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Configurar o ambiente do Android Studio
1. Criar um novo projeto do Android Studio e aceite os padrões de saudação no Assistente de saudação.
   
    ![Criar novo projeto no Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Dispositivos Android de destino](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Adicionar uma atividade toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset seus módulos de projeto, mover Olá clonado repositório toohello projeto local. Você também pode criar projeto hello e, em seguida, clone-a diretamente toohello local do projeto.
   
    ![Módulos do projeto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Abra as configurações de módulos de projeto de saudação usando o menu de contexto de saudação ou usando o atalho do hello Ctrl + Alt + lin + S.
   
    ![Configurações dos módulos do projeto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Remova o módulo de aplicativo padrão Olá porque desejar somente as configurações de contêiner de projeto hello.
   
    ![módulo de aplicativo Hello padrão](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Importar os módulos de projeto atual do toohello Olá repositório clonado.
   
    ![Importar o projeto de gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![criar a nova página de módulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Repita essas etapas para Olá `oidlib-sample` módulo.
7. Verificar dependências oidclib Olá Olá `oidlib-sample` módulo.
   
    ![dependências de oidclib no módulo de oidlib exemplo hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Clique em **OK** e aguarde a sincronização do gradle.
   
    O settings.gradle deve se parecer com este:
   
    ![Captura de tela de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Criar toomake de aplicativo de exemplo de hello-se de que esse exemplo hello sendo executado corretamente.
   
    Você não será capaz de toouse isso com o Azure Active Directory ainda. Vamos precisar tooconfigure alguns pontos de extremidade primeiro. Isso é tooensure você não tiver um problemas de Android Studio antes de começar a personalizar o aplicativo de exemplo hello.
10. Compilar e executar `oidlib-sample` como destino Olá no Android Studio.
    
    ![Progresso da criação do exemplo oidlib](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Excluir Olá `app ` diretório que foi deixado quando módulo Olá é removido do projeto Olá porque Android Studio não excluí-la para segurança.
    
    ![Estrutura do arquivo que contém o diretório de aplicativo hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Olá abrir **editar configurações** configuração Olá executado do menu tooremove que também foi deixada quando removido o módulo de saudação do projeto de saudação.
    
    ![Menu Editar configurações](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Executar configuração do aplicativo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Configurar pontos de extremidade de saudação do exemplo hello
Agora que você tem Olá `oidlib-sample` em execução com êxito, vamos Editar tooget alguns pontos de extremidade isso funcionar com o Active Directory do Azure.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Configurar o cliente editando o arquivo de oidc_clientconf.xml Olá
1. Porque você está usando OAuth2 de fluxos apenas tooget um token e chamar hello API do Graph, defina Olá cliente toodo OAuth2 somente. O OIDC aparecerá em um exemplo mais adiante.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Configure sua ID de cliente que você recebeu do portal de registro de saudação.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. Configure o URI de redirecionamento com hello um abaixo.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Configure os escopos que você precisa em ordem tooaccess Olá API do Graph.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Olá `User.Read` valor em `oidc_scopes` permite que você tooread Olá perfil básico Olá usuário conectado.
Você pode aprender mais sobre todos os escopos disponíveis de saudação em [escopos de permissão do Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Se você quiser explicações sobre `openid` ou `offline_access` como escopos no OpenID Connect, confira [Protocolos v2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Configurar seus pontos de extremidade do cliente, editando o arquivo de oidc_endpoints.xml Olá
* Olá abrir `oidc_endpoints.xml` de arquivo e fazer Olá as seguintes alterações:
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

Esses pontos de extremidade nunca deverão ser alterados se você estiver usando o OAuth2 como seu protocolo.

> [!NOTE]
> Olá pontos de extremidade para `userInfoEndpoint` e `revocationEndpoint` atualmente não são suportados pelo Active Directory do Azure. Se você deixar esses recursos com valor de example.com saudação padrão, você será lembrado que eles não estão disponíveis no exemplo hello :-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Configurar uma chamada à API do Graph
* Olá abrir `HomeActivity.java` de arquivo e fazer Olá as seguintes alterações:
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

Aqui, uma chamada simples à API do Graph retorna nossas informações.

Essas são todas as alterações de saudação que você precisa toodo. Executar Olá `oidlib-sample` aplicativo e clique em **entrar**.

Depois que você foi autenticado com êxito, selecione Olá **solicitar o recurso protegido** botão tootest toohello sua chamada de API do Graph.

## <a name="get-security-updates-for-our-product"></a>Obter atualizações de segurança para nosso produto
Recomendamos que você tooget notificações sobre incidentes de segurança visitando Olá [TechCenter de segurança](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.

