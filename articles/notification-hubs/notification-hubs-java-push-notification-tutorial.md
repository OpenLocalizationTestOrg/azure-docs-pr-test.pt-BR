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
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="6dce1-103">Como toouse Hubs de notificação do Java</span><span class="sxs-lookup"><span data-stu-id="6dce1-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="6dce1-104">Este tópico descreve os principais recursos de saudação do oficial Olá novo suportada total SDK de Java de Hub de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="6dce1-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="6dce1-105">Este é um projeto de código-fonte aberto e você pode exibir todo código SDK Olá em [Java SDK].</span><span class="sxs-lookup"><span data-stu-id="6dce1-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="6dce1-106">Em geral, você pode acessar todos os recursos de Hubs de notificação de um back-end do Java/PHP/Python/Ruby usando a interface REST do Hub de notificação de hello conforme descrito no tópico do MSDN Olá [APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="6dce1-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="6dce1-107">Esse SDK Java fornece um wrapper estreito em relação a essas interfaces REST em Java.</span><span class="sxs-lookup"><span data-stu-id="6dce1-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="6dce1-108">Olá SDK oferece suporte atualmente:</span><span class="sxs-lookup"><span data-stu-id="6dce1-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="6dce1-109">CRUD em Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="6dce1-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="6dce1-110">CRUD nos registros</span><span class="sxs-lookup"><span data-stu-id="6dce1-110">CRUD on Registrations</span></span>
* <span data-ttu-id="6dce1-111">Gerenciamento de instalação</span><span class="sxs-lookup"><span data-stu-id="6dce1-111">Installation Management</span></span>
* <span data-ttu-id="6dce1-112">Os registros de importação/exportação</span><span class="sxs-lookup"><span data-stu-id="6dce1-112">Import/Export Registrations</span></span>
* <span data-ttu-id="6dce1-113">Envio regular</span><span class="sxs-lookup"><span data-stu-id="6dce1-113">Regular Sends</span></span>
* <span data-ttu-id="6dce1-114">Envio agendado</span><span class="sxs-lookup"><span data-stu-id="6dce1-114">Scheduled Sends</span></span>
* <span data-ttu-id="6dce1-115">Operações assíncronas via NIO Java</span><span class="sxs-lookup"><span data-stu-id="6dce1-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="6dce1-116">Plataformas com suporte: APNS (iOS), GCM (Android), WNS (aplicativos da Windows Store), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android sem serviços do Google)</span><span class="sxs-lookup"><span data-stu-id="6dce1-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="6dce1-117">Uso do SDK</span><span class="sxs-lookup"><span data-stu-id="6dce1-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="6dce1-118">Compilação e construção</span><span class="sxs-lookup"><span data-stu-id="6dce1-118">Compile and build</span></span>
<span data-ttu-id="6dce1-119">Usar [Maven]</span><span class="sxs-lookup"><span data-stu-id="6dce1-119">Use [Maven]</span></span>

<span data-ttu-id="6dce1-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="6dce1-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="6dce1-121">Código</span><span class="sxs-lookup"><span data-stu-id="6dce1-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="6dce1-122">CRUDs do Hub de notificação</span><span class="sxs-lookup"><span data-stu-id="6dce1-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="6dce1-123">**Crie um Gerenciador de namespace:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="6dce1-124">**Crie o Hub de Notificação:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="6dce1-125">OU</span><span class="sxs-lookup"><span data-stu-id="6dce1-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="6dce1-126">**Obter Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="6dce1-127">**Atualizar Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="6dce1-128">**Excluir Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="6dce1-129">CRUDs de registro</span><span class="sxs-lookup"><span data-stu-id="6dce1-129">Registration CRUDs</span></span>
<span data-ttu-id="6dce1-130">**Crie um cliente do Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="6dce1-131">**Crie o registro do Windows:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="6dce1-132">**Crie registro do iOS:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="6dce1-133">Da mesma forma, você pode criar registros para Android (GCM), Windows Phone (MPNS) e Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="6dce1-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="6dce1-134">**Crie registros de modelo:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="6dce1-135">**Crie registros usando o padrão create registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="6dce1-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="6dce1-136">Remove duplicatas devido respostas tooany perdido se armazenar ids de registro no dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="6dce1-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="6dce1-137">**Atualize os registros:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="6dce1-138">**Exclua os registros:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="6dce1-139">**Registros de consulta:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-139">**Query registrations:**</span></span>

* <span data-ttu-id="6dce1-140">**Obter um registro único:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="6dce1-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="6dce1-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="6dce1-142">**Obter todos os registros no hub:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="6dce1-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="6dce1-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="6dce1-144">**Obter registros com marca:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="6dce1-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="6dce1-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="6dce1-146">**Obter registros por canal:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="6dce1-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="6dce1-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="6dce1-148">Todas as consultas de coleção suportam tokens $top e de continuação.</span><span class="sxs-lookup"><span data-stu-id="6dce1-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="6dce1-149">Uso da API de instalação</span><span class="sxs-lookup"><span data-stu-id="6dce1-149">Installation API usage</span></span>
<span data-ttu-id="6dce1-150">A API de instalação é um mecanismo alternativo para gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="6dce1-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="6dce1-151">Em vez de manter vários registros que não é tão simples e pode ser feito facilmente incorretamente ou ineficiente, agora é possível toouse um objeto de uma única instalação.</span><span class="sxs-lookup"><span data-stu-id="6dce1-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="6dce1-152">A instalação contém tudo o que você precisa: canal push (token de dispositivo), marcas, modelos, blocos secundários (para WNS e APNS).</span><span class="sxs-lookup"><span data-stu-id="6dce1-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="6dce1-153">Você não precisa mais toocall Olá serviço tooget Id - apenas gerar o GUID ou qualquer outro identificador, mantê-lo no dispositivo e enviar tooyour back-end junto com o canal de envio (token de dispositivo).</span><span class="sxs-lookup"><span data-stu-id="6dce1-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="6dce1-154">No back-end do hello, você deve fazer somente uma única chamada: CreateOrUpdateInstallation, ele é totalmente idempotentes, portanto se sentir livre tooretry se necessário.</span><span class="sxs-lookup"><span data-stu-id="6dce1-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="6dce1-155">Como exemplo, para o Amazon Kindle Fire ele tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="6dce1-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="6dce1-156">Se você quiser tooupdate-lo:</span><span class="sxs-lookup"><span data-stu-id="6dce1-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="6dce1-157">Para cenários avançados temos a capacidade de atualização parcial, que permite toomodify apenas as propriedades específicas do objeto de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dce1-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="6dce1-158">Basicamente, a atualização parcial é o subconjunto de operações de Patch JSON, que você pode executar no objeto de instalação.</span><span class="sxs-lookup"><span data-stu-id="6dce1-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="6dce1-159">Excluir a instalação:</span><span class="sxs-lookup"><span data-stu-id="6dce1-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="6dce1-160">CreateOrUpdate, Patch e Delete são eventualmente consistentes com Get.</span><span class="sxs-lookup"><span data-stu-id="6dce1-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="6dce1-161">A operação solicitada somente vai toohello fila do sistema durante a chamada de saudação e será executada em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="6dce1-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="6dce1-162">Observe que o Get não foi projetado para o cenário de tempo de execução principal, mas apenas para depuração e solução de problemas, ele rigidamente é limitado pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dce1-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="6dce1-163">Fluxo de envio para instalações é hello igual para registros.</span><span class="sxs-lookup"><span data-stu-id="6dce1-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="6dce1-164">Assim, apresentamos um toohello de notificação tootarget opção Instalação - basta usar marca "InstallationId: {desejado-id}".</span><span class="sxs-lookup"><span data-stu-id="6dce1-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="6dce1-165">Para o caso acima, ele ficaria assim:</span><span class="sxs-lookup"><span data-stu-id="6dce1-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="6dce1-166">Para um dos vários modelos:</span><span class="sxs-lookup"><span data-stu-id="6dce1-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="6dce1-167">Agendar notificações (disponível para a camada PADRÃO)</span><span class="sxs-lookup"><span data-stu-id="6dce1-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="6dce1-168">Olá mesmo como envio regular, mas com um parâmetro adicional - scheduledTime que informa quando a notificação deve ser entregue.</span><span class="sxs-lookup"><span data-stu-id="6dce1-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="6dce1-169">O serviço aceita qualquer ponto de tempo entre agora + 5 minutos e agora + 7 dias.</span><span class="sxs-lookup"><span data-stu-id="6dce1-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="6dce1-170">**Agendar uma notificação nativa do Windows:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="6dce1-171">Importação/exportação (disponível para a camada PADRÃO)</span><span class="sxs-lookup"><span data-stu-id="6dce1-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="6dce1-172">Às vezes, é necessário tooperform operação em massa registros.</span><span class="sxs-lookup"><span data-stu-id="6dce1-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="6dce1-173">Geralmente, é para a integração com outro sistema ou apenas uma correção grandes toosay atualização Olá as marcas.</span><span class="sxs-lookup"><span data-stu-id="6dce1-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="6dce1-174">É altamente não recomendável toouse fluxo de Get/atualização se estamos falando de milhares de registros.</span><span class="sxs-lookup"><span data-stu-id="6dce1-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="6dce1-175">O recurso de importação/exportação é o cenário de saudação do toocover projetado.</span><span class="sxs-lookup"><span data-stu-id="6dce1-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="6dce1-176">Basicamente, fornecem um contêiner de blob toosome acesso em sua conta de armazenamento como uma fonte de dados de entrada e de local de saída.</span><span class="sxs-lookup"><span data-stu-id="6dce1-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="6dce1-177">**Envie o trabalho de exportação:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="6dce1-178">**Envie o trabalho de importação:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="6dce1-179">**Aguarde até que o trabalho seja feito:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="6dce1-180">**Obter todos os trabalhos:**</span><span class="sxs-lookup"><span data-stu-id="6dce1-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="6dce1-181">**URI com assinatura SAS:** este é o URL de saudação de alguns arquivos de blob ou contêiner de blob mais o conjunto de parâmetros, como as permissões e a hora de expiração mais assinatura todas essas coisas feitas usando a chave SAS da conta.</span><span class="sxs-lookup"><span data-stu-id="6dce1-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="6dce1-182">O SDK Java do armazenamento do Azure tem recursos avançados, incluindo a criação de tal espécie de URIs.</span><span class="sxs-lookup"><span data-stu-id="6dce1-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="6dce1-183">Como alternativa simple, você pode dar uma olhada na classe de teste ImportExportE2E (a partir do local do github Olá) que tem uma implementação muito básica e compact do algoritmo de assinatura.</span><span class="sxs-lookup"><span data-stu-id="6dce1-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="6dce1-184">Enviar notificações</span><span class="sxs-lookup"><span data-stu-id="6dce1-184">Send Notifications</span></span>
<span data-ttu-id="6dce1-185">objeto de notificação de saudação é simplesmente um corpo com cabeçalhos, alguns métodos de utilitário ajudam na criação de objetos de saudação nativo e o modelo de notificações.</span><span class="sxs-lookup"><span data-stu-id="6dce1-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="6dce1-186">**Windows Store e Windows Phone 8.1 (não Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="6dce1-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="6dce1-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="6dce1-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="6dce1-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="6dce1-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="6dce1-189">**Silverlight para Windows Phone 8.0 e 8.1**</span><span class="sxs-lookup"><span data-stu-id="6dce1-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="6dce1-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="6dce1-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="6dce1-191">**Enviar tooTags**</span><span class="sxs-lookup"><span data-stu-id="6dce1-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="6dce1-192">**Enviar tootag expressão**</span><span class="sxs-lookup"><span data-stu-id="6dce1-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="6dce1-193">**Enviar notificação de modelo**</span><span class="sxs-lookup"><span data-stu-id="6dce1-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="6dce1-194">A execução do código Java agora deve produzir uma notificação que aparece no dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="6dce1-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="6dce1-195"><a name="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6dce1-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="6dce1-196">Neste tópico, mostramos como toocreate um Java simple REST cliente Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="6dce1-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="6dce1-197">A partir daqui, você pode:</span><span class="sxs-lookup"><span data-stu-id="6dce1-197">From here you can:</span></span>

* <span data-ttu-id="6dce1-198">Baixar Olá completo [Java SDK], que contém o código SDK inteiro hello.</span><span class="sxs-lookup"><span data-stu-id="6dce1-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="6dce1-199">Experimentar os exemplos de saudação:</span><span class="sxs-lookup"><span data-stu-id="6dce1-199">Play with hello samples:</span></span>
  * <span data-ttu-id="6dce1-200">[Introdução aos Hubs de Notificação]</span><span class="sxs-lookup"><span data-stu-id="6dce1-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="6dce1-201">[Enviar últimas notícias]</span><span class="sxs-lookup"><span data-stu-id="6dce1-201">[Send breaking news]</span></span>
  * <span data-ttu-id="6dce1-202">[Enviar últimas notícias localizadas]</span><span class="sxs-lookup"><span data-stu-id="6dce1-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="6dce1-203">[Enviar notificações aos usuários de tooauthenticated]</span><span class="sxs-lookup"><span data-stu-id="6dce1-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="6dce1-204">[Enviar notificações de plataforma cruzada tooauthenticated usuários]</span><span class="sxs-lookup"><span data-stu-id="6dce1-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Introdução aos Hubs de Notificação]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Enviar últimas notícias]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Enviar últimas notícias localizadas]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Enviar notificações aos usuários de tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Enviar notificações de plataforma cruzada tooauthenticated usuários]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

