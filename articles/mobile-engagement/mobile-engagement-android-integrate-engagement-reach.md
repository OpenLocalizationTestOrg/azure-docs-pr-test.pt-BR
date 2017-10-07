---
title: "aaaAzure integração do Mobile Engagement Android SDK"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>Como tooIntegrate contrato alcançam no Android
> [!IMPORTANT]
> Você deve seguir o procedimento de integração de saudação descrito em hello como tooIntegrate contrato no Android documento antes de seguir este guia.
> 
> 

## <a name="standard-integration"></a>Integração padrão

Copie os arquivos de recursos de alcance do hello SDK em seu projeto:

* Copiar arquivos de saudação do hello `res/layout` pasta entregues com hello SDK em Olá `res/layout` pasta do seu aplicativo.
* Copiar arquivos de saudação do hello `res/drawable` pasta entregues com hello SDK em Olá `res/drawable` pasta do seu aplicativo.

Edite seu arquivo `AndroidManifest.xml`:

* Adicionar Olá seção a seguir (entre hello `<application>` e `</application>` marcas):
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* Você precisa de notificações do sistema tooreplay essa permissão que não foram clicou na inicialização (caso contrário, eles serão mantidos no disco, mas não será mais exibidos, você realmente tem tooinclude isso).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Especificar um ícone usado para notificações (tanto no aplicativo e sistema aqueles) copiando e editando Olá seção a seguir (entre hello `<application>` e `</application>` marcas):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Esta seção é **obrigatória** se você planeja usar notificações de sistema durante a criação de campanhas de Alcance. O Android impede que as notificações de sistema sem ícones sejam exibidas. Portanto, se você omitir essa seção, os usuários finais não será capaz de tooreceive-los.
> 
> 

* Se você criar campanhas com notificações do sistema usando a visão geral, você precisa Olá tooadd as seguintes permissões (após Olá `</application>` marca) se ausentes:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * No Android M e se seu aplicativo direciona o nível de API de 23 do Android ou maior, a permissão do ``WRITE_EXTERNAL_STORAGE`` requer aprovação do usuário. Leia [esta seção](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Para notificações do sistema que você também pode especificar no hello alcançar campanha se dispositivo Olá deve tocar e/ou Vibrar. Para que ele toowork, você tem toomake-se de que você declarou Olá permissão a seguir (após Olá `</application>` marca):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Sem essa permissão, Android impede que as notificações do sistema de ser exibida se você tiver marcado anel hello ou hello Vibrar opção no Gerenciador de campanha de alcance hello.

## <a name="native-push"></a>Push nativo
Agora que você configurou o módulo de alcance, é necessário campanhas a tooconfigure push nativo toobe tooreceive capaz de saudação no dispositivo hello.

Oferecemos suporte a dois serviços no Android:

* Dispositivos do Google Play: Use [Google Cloud Messaging] pelo seguinte Olá [como tooIntegrate GCM com contrato guia](mobile-engagement-android-gcm-integrate.md) guia.
* Dispositivos do Amazon: Use [Amazon Device Messaging] pelo seguinte Olá [como tooIntegrate ADM com contrato guia](mobile-engagement-android-adm-integrate.md) guia.

Se você quiser tootarget dispositivos Amazon e Google Play, sua possíveis toohave tudo dentro de 1 AndroidManifest.xml/APK para desenvolvimento. Mas, ao enviar tooAmazon, eles podem rejeitar seu aplicativo se ele encontrar o código do GCM.

Nesse caso, você deve usar múltiplos APKs.

**Seu aplicativo está agora pronto tooreceive e exibição alcançar campanhas!**

## <a name="how-toohandle-data-push"></a>Como enviar por push dados toohandle
### <a name="integration"></a>Integração
Se você quiser toobe seu aplicativo capaz de envios tooreceive alcance dados, você tem toocreate uma subclasse de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` e referencie a saudação `AndroidManifest.xml` arquivo (entre hello `<application>` e/ou `</application>` marcas):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

Em seguida, você pode substituir Olá `onDataPushStringReceived` e `onDataPushBase64Received` retornos de chamada. Aqui está um exemplo:

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>Categoria
o parâmetro de categoria Olá é opcional quando você criar uma campanha de envio de dados e permite que você toofilter dados envia. Isso é útil se você tiver vários destinatários de difusão tratamento diferentes tipos de verificações de dados, ou se você quiser toopush diferentes tipos de `Base64` tooidentify de dados e desejar que seu tipo antes da análise-los.

### <a name="callbacks-return-parameter"></a>Parâmetro de retorno dos retornos de chamada
Aqui estão algumas diretrizes tooproperly identificador Olá parâmetro de retorno do `onDataPushStringReceived` e `onDataPushBase64Received`:

* Um receptor de difusão deve retornar `null` no retorno de chamada de saudação se ele não sabe como toohandle uma data de envio. Você deve usar o hello categoria toodetermine se o receptor difusão deve tratar dados por push-Olá ou não.
* Um receptor de difusão Olá deve retornar `true` no retorno de chamada de saudação se ele aceita o envio de dados de saudação.
* Um receptor de difusão Olá deve retornar `false` no retorno de chamada de saudação se reconhece os dados por push-Olá, mas descarta por qualquer motivo. Por exemplo, retornar `false` quando os dados recebido de saudação são inválidos.
* Se uma difusão do receptor retorna `true` enquanto outro um retorna `false` hello a mesma dados por push, o comportamento de saudação é indefinido, você nunca deve fazer isso.

tipo de retorno de saudação é usado apenas para estatísticas de alcance hello:

* `Replied`é incrementado se um dos receptores difusão Olá retornou um `true` ou `false`.
* `Actioned`é incrementado apenas se uma saudação difusão receptores retornados `true`.

## <a name="how-toocustomize-campaigns"></a>Como campanhas toocustomize
toocustomize campanhas, você pode modificar layouts de saudação fornecidos no hello SDK do Reach.

Você deve manter todos os identificadores de Olá usados em layouts de saudação e manter Olá tipos de exibições de saudação que usam um identificador, especialmente para modos de exibição de texto e imagem. Alguns modos de exibição são usado apenas toohide ou mostram as áreas para que seu tipo pode ser alterado. Verifique o código-fonte Olá se você pretende toochange tipo de saudação de uma exibição em layouts de saudação fornecido.

### <a name="notifications"></a>Notificações
Há dois tipos de notificações: as de sistema e aquelas contidas no aplicativo, que usam arquivos de layout diferentes.

#### <a name="system-notifications"></a>Notificações de sistema
notificações do sistema toocustomize necessário Olá toouse **categorias**. Você pode ir muito[categorias](#categories).

#### <a name="in-app-notifications"></a>Notificações no aplicativo
Por padrão, uma notificação no aplicativo é uma exibição que é adicionado dinamicamente toohello atual atividade usuário Obrigado toohello Android método de interface `addContentView()`. Isso é chamado uma sobreposição de notificação. Sobreposições de notificação são ótimas para uma integração rápida porque eles não requerem que você toomodify qualquer layout em seu aplicativo.

aparência de saudação toomodify de seu sobreposições de notificação, simplesmente modifique arquivo hello `engagement_notification_area.xml` tooyour precisa.

> [!NOTE]
> arquivo Hello `engagement_notification_overlay.xml` é Olá aquele toocreate usado em uma sobreposição de notificação, ele inclui o arquivo hello `engagement_notification_area.xml`. Você também pode personalizá-lo toosuit suas necessidades (como para a área de notificação de saudação em sobreposição de saudação de posicionamento).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Incluir um layout de notificação como parte de um layout de atividade
As sobreposições são ótimas para uma integração rápida, mas podem ser inconvenientes ou ter efeitos colaterais em casos especiais. Olá sobreposição sistema pode ser personalizado no nível de atividade, tornando fácil tooprevent efeito colateral de atividades especiais.

Você pode decidir tooinclude nosso layout de notificação no seu toohello de Obrigado layout existente Android **incluem** instrução. Olá, a seguir é um exemplo de uma modificação `ListActivity` layout que contêm apenas um `ListView`.

**Antes da integração do Engagement :**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Após a integração de Engagement :**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

Neste exemplo adicionamos um contêiner pai, pois layout original Olá usado um modo de exibição de lista como o elemento de nível superior hello. Também adicionamos `android:layout_weight="1"` tooadd capaz de toobe um modo de exibição abaixo de uma exibição de lista configurado com `android:layout_height="fill_parent"`.

Olá SDK do Reach contrato detecta automaticamente o layout de notificação que hello está incluído nesta atividade e não adicionará uma sobreposição para a atividade.

> [!TIP]
> Se você usar um ListActivity em seu aplicativo, uma sobreposição de alcance visível impedirá você de reagir a itens de tooclicked na exibição de lista hello mais. Esse é um problema conhecido. toowork alternativa para esse problema é recomendável tooembed layout de notificação de saudação em seu próprio layout de atividade de lista como no exemplo anterior de saudação.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Desabilitando a notificação de aplicativo por atividade
Se você não quiser Olá sobreposição toobe adicionado tooyour atividade e se você não incluir o layout de notificação de saudação em seu próprio layout, você pode desabilitar a sobreposição de saudação para esta atividade no hello `AndroidManifest.xml` adicionando um `meta-data` seção como no seguinte Olá exemplo:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a> Categorias
Quando você modifica Olá fornecido layouts, você modificar a aparência de saudação de todas as notificações. As categorias permitem que toodefine que vários direcionados parece (possivelmente comportamentos) para notificações. Uma categoria pode ser especificada quando você cria uma campanha de Reach. Tenha em mente que categorias também permitem personalizar anúncios e pesquisas, como está descrito mais adiante neste documento.

tooregister um manipulador de categoria para as notificações, você precisa tooadd uma chamada quando o aplicativo hello é inicializado.

> [!IMPORTANT]
> Leia o aviso de saudação sobre Olá android: atributo de \<android sdk-contrato processo\> em hello como tooIntegrate contrato no Android tópico antes de continuar.
> 
> 

Olá exemplo a seguir supõe que você confirmado aviso anterior hello e usa uma subclasse de `EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

Olá `MyNotifier` objeto é a implementação de saudação do manipulador de categoria de notificação de saudação. É qualquer uma implementação de saudação `EngagementNotifier` interface ou classe de implementação do padrão de saudação sub: `EngagementDefaultNotifier`.

Observe que mesmo Notificador de Olá pode lidar com várias categorias, você pode registrá-los como este:

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

implementação de categoria do tooreplace saudação padrão, você pode registrar sua implementação como no exemplo a seguir de saudação:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

Olá categoria usada em um manipulador é passada como um parâmetro na maioria dos métodos que você pode substituir na `EngagementDefaultNotifier`.

Ela é passada como um parâmetro `String` ou indiretamente em um objeto `EngagementReachContent` que tem um método `getCategory()`.

Você pode alterar a maior parte do processo de criação de notificação Olá redefinindo métodos em `EngagementDefaultNotifier`, para a personalização avançada se sentir livre tootake uma olhada na documentação técnica Olá e no código-fonte Olá.

##### <a name="in-app-notifications"></a>Notificações no aplicativo
Se você quiser apenas layouts alternativos toouse para uma categoria específica, você pode implementar isso como Olá exemplo a seguir:

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**Exemplo de `my_notification_overlay.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Como você pode ver, Olá identificador da exibição de sobreposição é diferente do padrão de saudação um. É importante que cada layout use um identificador exclusivo para sobreposições.

**Exemplo de `my_notification_area.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

Como você pode ver, identificador de exibição da área de notificação Olá é diferente do padrão de saudação um. É importante que cada layout use um identificador exclusivo para áreas de notificação.

Esse exemplo simples de categoria torna as notificações de aplicativos (ou no aplicativo) exibidas na parte superior de saudação da tela hello. Não alteramos identificadores padrão de saudação usados na área de notificação de saudação em si.

Se você quiser toochange, você tem Olá tooredefine `EngagementDefaultNotifier.prepareInAppArea` método. É recomendável toolook na documentação técnica Olá e no código-fonte saudação do `EngagementNotifier` e `EngagementDefaultNotifier` se desejar que esse nível de personalização avançada.

##### <a name="system-notifications"></a>Notificações de sistema
Estendendo `EngagementDefaultNotifier`, você pode substituir `onNotificationPrepared` notificação de saudação tooalter que foi preparada pela implementação do padrão de saudação.

Por exemplo:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

Este exemplo faz uma notificação do sistema para um conteúdo que está sendo exibido como um evento em andamento quando a categoria "em andamento" hello é usada.

Se você quiser Olá toobuild `Notification` do objeto do zero, você pode retornar `false` toohello método e chame `notify` por conta própria Olá `NotificationManager`. Nesse caso é importante que você mantenha um `contentIntent`, um `deleteIntent` e Olá identificador de notificação usado pelo `EngagementReachReceiver`.

Aqui está um exemplo correto de tal implementação:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>Anúncios exclusivamente de notificação
Olá gerenciamento de saudação clique em uma notificação de anúncio só pode ser personalizado, substituindo `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify Olá preparado `Intent`. Usando esse método permite que você tootune sinalizadores de saudação facilmente.

Por exemplo tooadd Olá `SINGLE_TOP` sinalizador:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Para usuários de contrato herdados, observe que as notificações do sistema sem ação URL agora inicia o aplicativo hello se estava no plano de fundo, para que esse método pode ser chamado com um anúncio sem a URL da ação. Você deve considerar isso ao personalizar a intenção de saudação.

Você também pode implementar o `EngagementNotifier.executeNotifAnnouncementAction` do zero.

##### <a name="notification-life-cycle"></a>Ciclo de vida de notificação
Ao usar a categoria de padrão de saudação, alguns métodos de ciclo de vida são chamados em Olá `EngagementReachInteractiveContent` tooreport estatísticas e atualização Olá campanha o estado do objeto:

* Quando notificação Olá é exibida no aplicativo ou colocar na barra de status hello, Olá `displayNotification` método é chamado (que relata estatísticas) por `EngagementReachAgent` se `handleNotification` retorna `true`.
* Se a notificação de saudação é ignorada, Olá `exitNotification` método é chamado, a estatística é relatada e campanhas Avançar agora podem ser processadas.
* Se a notificação de saudação é clicada, `actionNotification` é chamado, a estatística é relatada e intenção Olá associado é iniciada.

Se sua implementação de `EngagementNotifier` bypasses Olá comportamento padrão, você terá que toocall esses métodos de ciclo de vida por si mesmo. Olá exemplos a seguir ilustra alguns casos em que o comportamento padrão de saudação é ignorado:

* Você não precisa estender `EngagementDefaultNotifier`, por exemplo, você implementou o tratamento de categoria a partir do zero.
* Para notificações do sistema, você substitui Olá `onNotificationPrepared` e você tiver modificado `contentIntent` ou `deleteIntent` em Olá `Notification` objeto.
* Para notificações no aplicativo, você substitui `prepareInAppArea`, ser toomap-se de que pelo menos `actionNotification` tooone dos controles U.I.

> [!NOTE]
> Se `handleNotification` lançará uma exceção, Olá conteúdo será excluído e `dropContent` é chamado. Isso é informado nas estatísticas e as próximas campanhas agora podem ser processadas.
> 
> 

### <a name="announcements-and-polls"></a>Anúncios e pesquisas
#### <a name="layouts"></a>Layouts
Você pode modificar Olá `engagement_text_announcement.xml`, `engagement_web_announcement.xml` e `engagement_poll.xml` toocustomize anúncios de texto, notificações de web e pesquisas de arquivos.

Esses arquivos compartilham dois layouts comuns para a área de título hello e área do botão hello. Olá layout Título Olá é `engagement_content_title.xml` e usa Olá eponymous arquivo drawable para plano de fundo de saudação. Olá layout para os botões de ação e sair de saudação é `engagement_button_bar.xml` e usa Olá eponymous arquivo drawable para plano de fundo de saudação.

Em uma pesquisa, Olá layout de pergunta e as opções são aumentadas dinamicamente usando várias vezes Olá `engagement_question.xml` arquivo de layout para perguntas hello e hello `engagement_choice.xml` arquivo para obter opções de saudação.

#### <a name="categories"></a>Categorias
##### <a name="alternate-layouts"></a>Layouts alternativos
Como as notificações, categoria da campanha Olá pode ser usado toohave de layouts alternativos para suas notificações e pesquisas.

Por exemplo, toocreate uma categoria para um anúncio de texto, você pode estender `EngagementTextAnnouncementActivity` e referencie-Olá `AndroidManifest.xml` arquivo:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Observe a categoria Olá no intenção de saudação filtro é usado toomake diferença hello atividade de anúncio saudação padrão.

Olá SDK do Reach usa Olá intenção tooresolve Olá direito a atividade do sistema para uma categoria específica e ele volta na categoria de padrão de saudação se Olá resolução falhou.

Em seguida, você tem tooimplement `MyCustomTextAnnouncementActivity`, se você apenas deseja toochange layout de saudação (mas lembre-Olá mesmo exibir identificadores), você tem apenas classe de saudação toodefine como no exemplo a seguir de saudação:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

categoria de padrão de saudação tooreplace de anúncios de texto, basta substituir `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` pela sua implementação.

Pesquisas e anúncios da Web podem ser personalizadas de modo semelhante.

Para notificações de web, você pode estender `EngagementWebAnnouncementActivity` e declarar sua atividade no hello `AndroidManifest.xml` como no exemplo a seguir de saudação:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

Para pesquisas, você pode estender `EngagementPollActivity` e declarar o hello em `AndroidManifest.xml` como no exemplo a seguir de saudação:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Implementação do zero
Você pode implementar categorias para suas atividades de anúncio (e pesquisa) sem estender uma saudação `Engagement*Activity` classes fornecidas pela Olá SDK do Reach. Isso é útil por exemplo se você quiser toodefine um layout que não usa Olá mesmo exibições como layouts de saudação padrão.

Como personalização avançada de notificação, é recomendável toolook no código-fonte da implementação padrão Olá Olá.

Aqui estão algumas coisas tookeep em mente: alcance iniciará atividade Olá com um propósito específico (toohello intenção filtro correspondente) além de um parâmetro extra que é o identificador de conteúdo de saudação.

tooretrieve Olá objeto do conteúdo que contêm campos de saudação especificado quando criar hello da campanha no site Olá você pode fazer isso:

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

Para estatísticas, você pode relatar Olá conteúdo é exibido em Olá `onResume` evento:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

Em seguida, não se esqueça de toocall ou `actionContent(this)` ou `exitContent(this)` no objeto de conteúdo de saudação antes de atividade Olá entra no plano de fundo.

Se você não chamar o `actionContent` ou `exitContent`, as estatísticas não serão enviadas (ou seja, nenhuma análise campanha Olá) e mais importante, Olá campanhas próximas não serão notificadas até que o processo de aplicativo hello seja reiniciado.

Orientação ou outras alterações de configuração pode tomar Olá código complicado toodetermine atividade Olá entra no plano de fundo ou não, Olá torna a implementação padrão se conteúdo de saudação é relatado como encerrado se Olá usuário deixar uma atividade de saudação (seja por pressionar `HOME` ou `BACK`) mas não se altera a orientação de saudação.

Aqui está a parte interessante Olá implementação Olá:

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

Como você pode ver, se você chamou `actionContent(this)` depois de terminar a atividade de saudação `exitContent(this)` pode ser chamado com segurança sem causar qualquer impacto.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
