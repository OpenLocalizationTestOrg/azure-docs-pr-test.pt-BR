---
title: aaaHow tooenable SSO entre aplicativo no Android usando o ADAL | Microsoft Docs
description: "Como toouse recursos de saudação do hello tooenable SDK ADAL logon único em seus aplicativos. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a>Como tooenable SSO entre aplicativo no Android usando o ADAL
Fornecer Single Sign-On (SSO) para que usuários só precisam tooenter suas credenciais de uma vez e tem as credenciais de trabalho automaticamente em todos os aplicativos agora é esperado por clientes. Dificuldade de saudação inserir seu nome de usuário e senha em uma tela pequena, geralmente vezes combinados com um fator adicional (2FA) como uma chamada telefônica ou um código enviado por texto, resulta em insatisfação rápida se um usuário tem toodo isso mais de uma vez para o seu produto.

Além disso, se você aplicar uma plataforma de identidade que outros aplicativos podem usar como Accounts da Microsoft ou uma conta de trabalho do Office 365, os clientes esperam que os toobe de credenciais disponíveis toouse em todos os seus aplicativos não importa fornecedor hello.

Olá plataforma do Microsoft Identity, juntamente com nossos SDKs de identidade da Microsoft, tudo isso funciona rígido para você e fornece a você Olá capacidade toodelight seus clientes com o SSO em seu próprio conjunto de aplicativos ou, como com nosso recurso de agente e um autenticador aplicativos, em todo dispositivo de saudação.

Este passo a passo mostrará como tooconfigure nossa SDK em seu aplicativo tooprovide clientes de tooyour esse benefício.

Este passo a passo se aplica a:

* Azure Active Directory
* Active Directory B2C do Azure
* Azure Active Directory B2B
* Acesso condicional ao Azure Active Directory

documento de saudação anterior pressupõe que você sabe como muito[provisionar aplicativos no portal herdados de saudação do Azure Active Directory](active-directory-how-to-integrate.md) e seu aplicativo integrado com hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android) .

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Conceitos de SSO em Olá plataforma de identidade da Microsoft
### <a name="microsoft-identity-brokers"></a>Agentes do Microsoft Identity
Microsoft oferece aos aplicativos para cada plataforma móvel que permitem Olá ponte de credenciais nos aplicativos de fornecedores diferentes e permite recursos aprimorados especiais que exigem um único local seguro de onde toovalidate credenciais. Chamamos esses recursos de **agentes**. No iOS e Android, eles são fornecidos por meio de aplicativos para download que os clientes instalar independente ou podem ser enviados toohello dispositivo por uma empresa que gerencia alguns ou todos os dispositivos de saudação para seus funcionários. Esses agentes dão suporte à segurança de gerenciamento apenas para alguns aplicativos ou todo dispositivo de saudação com base no qual os administradores de TI deseja. No Windows, essa funcionalidade é fornecida por um seletor de conta interna do sistema operacional de toohello, tecnicamente conhecido como Olá agente de autenticação da Web.

Para obter mais informações sobre como usamos esses agentes e como os clientes podem vê-los em seu fluxo de logon para a plataforma do Microsoft Identity Olá ler no.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>Padrões de logon em dispositivos móveis
Acesso toocredentials em dispositivos execute dois padrões básicos para a plataforma do Microsoft Identity hello:

* Logons assistidos por não agentes
* Logons assistidos por agentes

#### <a name="non-broker-assisted-logins"></a>Logons assistidos por não agentes
Logons de agente não assistidos são experiências de logon que ocorrem em linha com o aplicativo hello e usam o armazenamento local de saudação no dispositivo Olá para o aplicativo. Esse armazenamento pode ser compartilhado entre aplicativos, mas credenciais de saudação estão estreitamente acoplado toohello aplicativo ou pacote de aplicativos que usam essa credencial. Você provavelmente já passou isso em muitos aplicativos móveis quando você inserir um nome de usuário e senha dentro do próprio aplicativo hello.

Esses logons têm Olá benefícios a seguir:

* Experiência do usuário existe completamente no aplicativo hello.
* As credenciais podem ser compartilhadas entre aplicativos que são assinados por Olá mesmo certificado, fornecendo um conjunto de tooyour experiência de logon único de aplicativos.
* Controle de experiência de saudação de logon é fornecido toohello aplicativo antes e depois de entrar.

Esses logons têm Olá seguintes desvantagens:

* O usuário não consegue experimentar o logon único em todos os aplicativos que usam um Microsoft Identity, somente entre os Microsoft Identities configurados por seu aplicativo.
* O aplicativo não pode ser usado com recursos mais avançados de negócios, como acesso condicional ou use Olá InTune pacote de produtos.
* Seu aplicativo não dá suporte à autenticação baseada em certificado para usuários corporativos.

Aqui está uma representação de como os SDKs de identidade do Microsoft hello funcionam com armazenamento Olá compartilhado de sua tooenable aplicativos SSO:

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>Logons assistidos por agentes
Logons assistido por agente são experiências de logon que ocorrem no aplicativo de broker hello e usam armazenamento hello e segurança de credenciais do hello broker tooshare em todos os aplicativos no dispositivo de saudação que se aplicam a plataforma do Microsoft Identity hello. Isso significa que seus aplicativos usam Olá broker toosign usuários. No iOS e Android esses agentes são fornecidos por meio de aplicativos para download que os clientes instalar independente ou podem ser enviados toohello dispositivo por uma empresa que gerencia o dispositivo Olá para o usuário. Um exemplo desse tipo de aplicativo é um aplicativo do Microsoft Authenticator hello no iOS. No Windows, essa funcionalidade é fornecida por um seletor de conta interna do sistema operacional de toohello, tecnicamente conhecido como Olá agente de autenticação da Web.
experiência de saudação varia por plataforma e às vezes pode ser toousers interrupções se não gerenciados corretamente. Você provavelmente está mais familiarizado com esse padrão se você tiver o aplicativo do Facebook hello instalado e usa o Facebook Connect de outro aplicativo. Olá, usos de plataforma do Microsoft Identity Olá mesmo padrão.

Para iOS isso leva animação de "transição" tooa onde seu aplicativo é enviado toohello em segundo plano enquanto os aplicativos do Microsoft Authenticator Olá vem toohello em primeiro plano para Olá usuário tooselect qual conta gostariam toosign com.  

Para a conta de saudação do Android e Windows seletor é exibida na parte superior de seu aplicativo de usuário de toohello menos interrupções.

#### <a name="how-hello-broker-gets-invoked"></a>Como o agente de saudação obtém chamado
Se um agente compatível estiver instalado no dispositivo hello, como Olá aplicativo Microsoft Authenticator, Olá SDKs do Microsoft Identity será automaticamente Olá invocar broker Olá para você quando um usuário indica desejarem toolog usando qualquer conta de trabalho plataforma do Microsoft Identity Hello. Essa conta pode ser uma Conta da Microsoft pessoal, uma conta corporativa ou de estudante ou uma conta que você fornece e hospeda no Azure usando nossos produtos B2C e B2B. 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a>Como podemos garantir que o aplicativo hello é válido
 
 Olá necessidade tooensure Olá identidade um agente do aplicativo chamada hello é crucial toohello segurança que fornecemos em logons de broker assistido. IOS, nem Android impõe identificadores exclusivos que só são válidos para um determinado aplicativo, para que aplicativos mal-intencionados podem "falsificar" identificador de um aplicativo legítimo e receber tokens Olá destinam-se para o aplicativo legítimo hello. tooensure que é sempre se comunicam com o aplicativo correto hello em tempo de execução, solicitamos Olá desenvolvedor tooprovide um redirectURI personalizado ao registrar seu aplicativo com a Microsoft. **O modo como os desenvolvedores devem criar esse URI de redirecionamento será abordado com detalhes logo abaixo.** Este redirectURI personalizado contém a impressão digital do certificado de saudação do aplicativo hello e é garantido toobe toohello exclusivo aplicativo pela Olá Google Play Store. Quando um aplicativo chama broker hello, broker Olá solicita tooprovide do sistema operacional Android Olá com hello impressão digital do certificado que broker chamado hello. broker Olá fornece essa tooMicrosoft de impressão digital do certificado no sistema de identidade Olá chamada tooour. Se certificado Olá impressão digital do aplicativo hello não coincide com a impressão digital do certificado Olá fornecido toous pelo desenvolvedor Olá durante o registro, podemos negará o acesso toohello tokens para Olá recurso Olá aplicativo está solicitando. Essa verificação garante que apenas aplicativo hello registrado pelo desenvolvedor Olá recebe tokens.

**desenvolvedor Olá possui escolha de saudação do se Olá SDK do Microsoft Identity chama broker hello ou usa Olá sem agente assistido fluxo.** No entanto se o desenvolvedor de saudação escolher não toouse Olá assistido broker fluxo percam benefício de saudação do uso de credenciais de SSO usuário Olá já tenha adicionado no dispositivo hello e impede que seu aplicativo está sendo usado com recursos da empresa Microsoft oferece a seus clientes, como acesso condicional, recursos de gerenciamento do Intune e autenticação baseada em certificado.

Esses logons têm Olá benefícios a seguir:

* Usuário experiências SSO entre todos os seus aplicativos, independentemente do fornecedor de saudação.
* Seu aplicativo pode usar recursos de negócios mais avançados como acesso condicional ou conjunto de InTune Olá de produtos.
* Seu aplicativo pode oferecer suporte à autenticação baseada em certificado para usuários corporativos.
* Muito mais segura experiência de entrada no como identidade de saudação do aplicativo hello e usuário Olá sejam verificadas pelo aplicativo de broker hello com criptografia e algoritmos de segurança adicional.

Esses logons têm Olá seguintes desvantagens:

* No iOS usuário Olá foi transicionado fora do processo do aplicativo enquanto as credenciais são escolhidas.
* Perda de logon de Olá Olá capacidade toomanage experiência para os clientes dentro de seu aplicativo.

Aqui está uma representação de como Olá SDKs do Microsoft Identity trabalho com hello broker tooenable aplicativos SSO:

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

Com essas informações de plano de fundo deve ser capaz de toobetter entender e implementar o SSO dentro de seu aplicativo usando a plataforma do Microsoft Identity hello e SDKs.

## <a name="enabling-cross-app-sso-using-adal"></a>Habilitar SSO entre aplicativos usando a ADAL
Aqui usamos Olá ADAL SDK do Android para:

* Ativar o SSO assistido por não agente para seu pacote de aplicativos
* Ativar o suporte para SSO assistido por agente

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Ativar o SSO assistido por não agente
Para SSO de assistido sem agente em todos os aplicativos Olá SDKs do Microsoft Identity gerenciar grande parte da complexidade de saudação do SSO para você. Isso inclui localizar usuário Olá no cache de saudação e manter uma lista de usuários conectados para você tooquery.

tooenable SSO entre os aplicativos que você possui que precisar Olá toodo a seguir:

1. Verifique se todos os seu aplicativos usuário Olá mesma ID de cliente ou a ID do aplicativo.
2. Certifique-se de que todos os seus aplicativos tenham Olá que mesmo SharedUserID definido.
3. Certifique-se de que todos os seu Olá de compartilhamento de aplicativos mesmo certificado de autenticação do Google Play da saudação armazenar para que você pode compartilhar o armazenamento.

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Etapa 1: Usando Olá a mesma ID de cliente / ID de aplicativo para todos os aplicativos em seu pacote de aplicativos de Olá
Para tooknow de plataforma do Microsoft Identity Olá que é permitido tooshare tokens em seus aplicativos, cada um dos aplicativos precisará tooshare Olá mesma ID de cliente ou a ID do aplicativo. Este é o identificador exclusivo de saudação fornecida tooyou quando você registrou seu primeiro aplicativo no portal de saudação.

Você deve estar se perguntando como você identificará os diferentes aplicativos toohello serviço do Microsoft Identity se ele usa Olá ID do mesmo aplicativo. resposta de saudação é com hello **URIs de redirecionamento**. Cada aplicativo pode ter vários URIs de redirecionamento registrado no portal de integração de saudação. Cada aplicativo em seu pacote terá um URI de redirecionamento diferente. Veja abaixo um exemplo de como isso acontece.

URI de Redirecionamento do App1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`

URI de Redirecionamento do App2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`

URI de Redirecionamento do App3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`

....

Esses são aninhados em Olá a mesma ID de cliente / ID do aplicativo e pesquisada Olá com base em redirecionam URI retornar toous em sua configuração de SDK.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*Observe que o formato desses URIs de redirecionamento de Olá são explicados abaixo. Você pode usar qualquer URI de redirecionamento, a menos que você deseja que o agente de saudação toosupport, caso em que eles devem ter a aparência Olá acima*

#### <a name="step-2-configuring-shared-storage-in-android"></a>Etapa 2: Configurando o armazenamento compartilhado no Android
Saudação de configuração `SharedUserID` está além do escopo deste documento hello, mas podem ser aprendidos lendo Olá documentação Google Android Olá [manifesto](http://developer.android.com/guide/topics/manifest/manifest-element.html). O importante é que você decida qual o nome de seu sharedUserID e usar esse nome em todos os seus aplicativos.

Depois que você tiver Olá `SharedUserID` em todos os seus aplicativos, você está pronto toouse SSO.

> [!WARNING]
> Quando você compartilhar o armazenamento em seus aplicativos de qualquer aplicativo pode excluir usuários ou pior excluir todos os tokens de saudação em seu aplicativo. Isso é particularmente desastroso se você tiver aplicativos que dependem de trabalho em segundo plano do hello tokens toodo. Compartilhamento de armazenamento significa que você seja muito cuidado ao remover todas as operações por meio de saudação SDKs do Microsoft Identity.
> 
> 

É isso! Olá SDK do Microsoft Identity agora compartilharão as credenciais em todos os seus aplicativos. lista de saudação do usuário também será compartilhada entre instâncias do aplicativo.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>Ativar o SSO assistido por agente
Olá capacidade para um toouse de aplicativo é qualquer agente instalado no dispositivo Olá **desativado por padrão**. Em ordem toouse seu aplicativo com o agente de saudação fazer algumas configurações adicionais e adicionar algum aplicativo tooyour de código.

Olá etapas toofollow são:

1. Habilitar o modo de agente na toohello de chamada do código do aplicativo SDK MS
2. Estabelecer um novo URI de redirecionamento e fornecer o aplicativo hello tooboth e seu registro de aplicativo
3. Configurando permissões corretas de saudação no manifesto do Android Olá

#### <a name="step-1-enable-broker-mode-in-your-application"></a>Etapa 1: habilitar o modo de agente em seu aplicativo
capacidade de saudação para o agente do aplicativo toouse Olá é ativada quando você cria configurações"hello" ou a configuração inicial da sua instância de autenticação. Faça isso configurando o tipo ApplicationSettings em seu código:

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a>Etapa 2: Estabelecer um novo URI de redirecionamento com seu esquema de URL
Tooensure ordem que estamos sempre retornar credencial Olá tokens de aplicativo correto toohello, precisamos toomake se que chamar novamente tooyour aplicativo de forma que Olá sistema operacional Android pode verificar. sistema de operacional Android Olá usa o hash de saudação do certificado de saudação em Olá loja Google Play. Isso não pode ser falsificado por um aplicativo mal-intencionado. Portanto, podemos utilizar isso junto com hello URI do nosso tooensure de aplicativo de agente que tokens Olá são retornados de aplicativo correto toohello. É necessário tooestablish você no seu aplicativo e defina o URI de redirecionamento exclusivo como um URI de redirecionamento em nosso portal do desenvolvedor.

O URI de redirecionamento deve estar no formato adequado de saudação do:

`msauth://packagename/Base64UrlencodedSignature`

ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*

Esse URI de redirecionamento precisa toobe especificado em seu registro de aplicativo usando Olá [portal do Azure](https://portal.azure.com/). Para saber mais sobre o registro de aplicativo do Azure AD, confira [Integração com o Azure Active Directory](active-directory-how-to-integrate.md).

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a>Etapa 3: Definir as permissões corretas de Olá em seu aplicativo
Nosso aplicativo de agente no Android usa o recurso de Gerenciador de contas de saudação de credenciais de toomanage de sistema operacional Android Olá entre aplicativos. No agente de saudação toouse ordem no Android o manifesto do aplicativo deve ter contas de AccountManager de toouse de permissões. Isso é discutido em detalhes no hello [Google documentação para o gerente de conta aqui](http://developer.android.com/reference/android/accounts/AccountManager.html)

Em particular, essas permissões são:

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a>Você configurou o SSO!
Agora Olá SDK do Microsoft Identity automaticamente as credenciais de compartilhamento em seus aplicativos e invocar broker Olá caso ele esteja presente em seu dispositivo.

