---
title: "aaaHow toouse Hubs de notificação com Java"
description: "Saiba como toouse Hubs de notificação do Azure de um back-end de Java."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a>Como toouse Hubs de notificação do Java
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Este tópico descreve os principais recursos de saudação do oficial Olá novo suportada total SDK de Java de Hub de notificação do Azure. Este é um projeto de código-fonte aberto e você pode exibir todo código SDK Olá em [Java SDK]. 

Em geral, você pode acessar todos os recursos de Hubs de notificação de um back-end do Java/PHP/Python/Ruby usando a interface REST do Hub de notificação de hello conforme descrito no tópico do MSDN Olá [APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn223264.aspx). Esse SDK Java fornece um wrapper estreito em relação a essas interfaces REST em Java. 

Olá SDK oferece suporte atualmente:

* CRUD em Hubs de notificação 
* CRUD nos registros
* Gerenciamento de instalação
* Os registros de importação/exportação
* Envio regular
* Envio agendado
* Operações assíncronas via NIO Java
* Plataformas com suporte: APNS (iOS), GCM (Android), WNS (aplicativos da Windows Store), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android sem serviços do Google) 

## <a name="sdk-usage"></a>Uso do SDK
### <a name="compile-and-build"></a>Compilação e construção
Usar [Maven]

toobuild:

    mvn package

## <a name="code"></a>Código
### <a name="notification-hub-cruds"></a>CRUDs do Hub de notificação
**Crie um Gerenciador de namespace:**

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

**Crie o Hub de Notificação:**

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 OU

    hub = new NotificationHub("connection string", "hubname");

**Obter Hub de notificação:**

    hub = namespaceManager.getNotificationHub("hubname");

**Atualizar Hub de notificação:**

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

**Excluir Hub de notificação:**

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a>CRUDs de registro
**Crie um cliente do Hub de notificação:**

    hub = new NotificationHub("connection string", "hubname");

**Crie o registro do Windows:**

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

**Crie registro do iOS:**

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

Da mesma forma, você pode criar registros para Android (GCM), Windows Phone (MPNS) e Kindle Fire (ADM).

**Crie registros de modelo:**

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

**Crie registros usando o padrão create registrationid + upsert**

Remove duplicatas devido respostas tooany perdido se armazenar ids de registro no dispositivo hello:

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

**Atualize os registros:**

    hub.updateRegistration(reg);

**Exclua os registros:**

    hub.deleteRegistration(regid);

**Registros de consulta:**

* **Obter um registro único:**
  
    hub.getRegistration(regid);
* **Obter todos os registros no hub:**
  
    hub.getRegistrations();
* **Obter registros com marca:**
  
    hub.getRegistrationsByTag("myTag");
* **Obter registros por canal:**
  
    hub.getRegistrationsByChannel("devicetoken");

Todas as consultas de coleção suportam tokens $top e de continuação.

### <a name="installation-api-usage"></a>Uso da API de instalação
A API de instalação é um mecanismo alternativo para gerenciamento de registro. Em vez de manter vários registros que não é tão simples e pode ser feito facilmente incorretamente ou ineficiente, agora é possível toouse um objeto de uma única instalação. A instalação contém tudo o que você precisa: canal push (token de dispositivo), marcas, modelos, blocos secundários (para WNS e APNS). Você não precisa mais toocall Olá serviço tooget Id - apenas gerar o GUID ou qualquer outro identificador, mantê-lo no dispositivo e enviar tooyour back-end junto com o canal de envio (token de dispositivo). No back-end do hello, você deve fazer somente uma única chamada: CreateOrUpdateInstallation, ele é totalmente idempotentes, portanto se sentir livre tooretry se necessário.

Como exemplo, para o Amazon Kindle Fire ele tem esta aparência:

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

Se você quiser tooupdate-lo: 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

Para cenários avançados temos a capacidade de atualização parcial, que permite toomodify apenas as propriedades específicas do objeto de instalação de saudação. Basicamente, a atualização parcial é o subconjunto de operações de Patch JSON, que você pode executar no objeto de instalação.

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

Excluir a instalação:

    hub.deleteInstallation(installation.getInstallationId());

CreateOrUpdate, Patch e Delete são eventualmente consistentes com Get. A operação solicitada somente vai toohello fila do sistema durante a chamada de saudação e será executada em segundo plano. Observe que o Get não foi projetado para o cenário de tempo de execução principal, mas apenas para depuração e solução de problemas, ele rigidamente é limitado pelo serviço de saudação.

Fluxo de envio para instalações é hello igual para registros. Assim, apresentamos um toohello de notificação tootarget opção Instalação - basta usar marca "InstallationId: {desejado-id}". Para o caso acima, ele ficaria assim:

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

Para um dos vários modelos:

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a>Agendar notificações (disponível para a camada PADRÃO)
Olá mesmo como envio regular, mas com um parâmetro adicional - scheduledTime que informa quando a notificação deve ser entregue. O serviço aceita qualquer ponto de tempo entre agora + 5 minutos e agora + 7 dias.

**Agendar uma notificação nativa do Windows:**

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a>Importação/exportação (disponível para a camada PADRÃO)
Às vezes, é necessário tooperform operação em massa registros. Geralmente, é para a integração com outro sistema ou apenas uma correção grandes toosay atualização Olá as marcas. É altamente não recomendável toouse fluxo de Get/atualização se estamos falando de milhares de registros. O recurso de importação/exportação é o cenário de saudação do toocover projetado. Basicamente, fornecem um contêiner de blob toosome acesso em sua conta de armazenamento como uma fonte de dados de entrada e de local de saída.

**Envie o trabalho de exportação:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


**Envie o trabalho de importação:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

**Aguarde até que o trabalho seja feito:**

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

**Obter todos os trabalhos:**

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

**URI com assinatura SAS:** este é o URL de saudação de alguns arquivos de blob ou contêiner de blob mais o conjunto de parâmetros, como as permissões e a hora de expiração mais assinatura todas essas coisas feitas usando a chave SAS da conta. O SDK Java do armazenamento do Azure tem recursos avançados, incluindo a criação de tal espécie de URIs. Como alternativa simple, você pode dar uma olhada na classe de teste ImportExportE2E (a partir do local do github Olá) que tem uma implementação muito básica e compact do algoritmo de assinatura.

### <a name="send-notifications"></a>Enviar notificações
objeto de notificação de saudação é simplesmente um corpo com cabeçalhos, alguns métodos de utilitário ajudam na criação de objetos de saudação nativo e o modelo de notificações.

* **Windows Store e Windows Phone 8.1 (não Silverlight)**
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* **iOS**
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* **Android**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* **Silverlight para Windows Phone 8.0 e 8.1**
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* **Kindle Fire**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* **Enviar tooTags**
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* **Enviar tootag expressão**       
  
        hub.sendNotification(n, "foo && ! bar");
* **Enviar notificação de modelo**
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

A execução do código Java agora deve produzir uma notificação que aparece no dispositivo de destino.

## <a name="next-steps"></a>Próximas etapas
Neste tópico, mostramos como toocreate um Java simple REST cliente Hubs de notificação. A partir daqui, você pode:

* Baixar Olá completo [Java SDK], que contém o código SDK inteiro hello. 
* Experimentar os exemplos de saudação:
  * [Introdução aos Hubs de Notificação]
  * [Enviar últimas notícias]
  * [Enviar últimas notícias localizadas]
  * [Enviar notificações aos usuários de tooauthenticated]
  * [Enviar notificações de plataforma cruzada tooauthenticated usuários]

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Introdução aos Hubs de Notificação]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Enviar últimas notícias]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Enviar últimas notícias localizadas]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Enviar notificações aos usuários de tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Enviar notificações de plataforma cruzada tooauthenticated usuários]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

