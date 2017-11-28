---
title: "Como usar Hubs de Notificação com Java"
description: "Aprenda a usar Hubs de notificação do Azure de um back-end do Java."
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
ms.openlocfilehash: 41f978750ddef9f7e878c65b0017e909720154aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-java"></a><span data-ttu-id="7eefe-103">Como usar os Hubs de notificação do Java</span><span class="sxs-lookup"><span data-stu-id="7eefe-103">How to use Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="7eefe-104">Este tópico descreve os principais recursos do totalmente novo do Java SDK do Hub de notificação do Azure com suporte oficial.</span><span class="sxs-lookup"><span data-stu-id="7eefe-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="7eefe-105">Este é um projeto de software livre e você pode exibir todo o código do SDK no [SDK do Java].</span><span class="sxs-lookup"><span data-stu-id="7eefe-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="7eefe-106">Normalmente, você pode acessar todos os recursos dos Hubs de Notificação por meio de um back-end de Java/PHP/Ruby usando a interface REST do Hub de Notificação, conforme descrito no tópico do MSDN [APIs REST dos Hubs de Notificação](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="7eefe-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="7eefe-107">Esse SDK Java fornece um wrapper estreito em relação a essas interfaces REST em Java.</span><span class="sxs-lookup"><span data-stu-id="7eefe-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="7eefe-108">O SDK oferece suporte atualmente:</span><span class="sxs-lookup"><span data-stu-id="7eefe-108">The SDK supports currently:</span></span>

* <span data-ttu-id="7eefe-109">CRUD em Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="7eefe-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="7eefe-110">CRUD nos registros</span><span class="sxs-lookup"><span data-stu-id="7eefe-110">CRUD on Registrations</span></span>
* <span data-ttu-id="7eefe-111">Gerenciamento de instalação</span><span class="sxs-lookup"><span data-stu-id="7eefe-111">Installation Management</span></span>
* <span data-ttu-id="7eefe-112">Os registros de importação/exportação</span><span class="sxs-lookup"><span data-stu-id="7eefe-112">Import/Export Registrations</span></span>
* <span data-ttu-id="7eefe-113">Envio regular</span><span class="sxs-lookup"><span data-stu-id="7eefe-113">Regular Sends</span></span>
* <span data-ttu-id="7eefe-114">Envio agendado</span><span class="sxs-lookup"><span data-stu-id="7eefe-114">Scheduled Sends</span></span>
* <span data-ttu-id="7eefe-115">Operações assíncronas via NIO Java</span><span class="sxs-lookup"><span data-stu-id="7eefe-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="7eefe-116">Plataformas com suporte: APNS (iOS), GCM (Android), WNS (aplicativos da Windows Store), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android sem serviços do Google)</span><span class="sxs-lookup"><span data-stu-id="7eefe-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="7eefe-117">Uso do SDK</span><span class="sxs-lookup"><span data-stu-id="7eefe-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="7eefe-118">Compilação e construção</span><span class="sxs-lookup"><span data-stu-id="7eefe-118">Compile and build</span></span>
<span data-ttu-id="7eefe-119">Usar [Maven]</span><span class="sxs-lookup"><span data-stu-id="7eefe-119">Use [Maven]</span></span>

<span data-ttu-id="7eefe-120">Para construir:</span><span class="sxs-lookup"><span data-stu-id="7eefe-120">To build:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="7eefe-121">Código</span><span class="sxs-lookup"><span data-stu-id="7eefe-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="7eefe-122">CRUDs do Hub de notificação</span><span class="sxs-lookup"><span data-stu-id="7eefe-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="7eefe-123">**Crie um Gerenciador de namespace:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="7eefe-124">**Crie o Hub de Notificação:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="7eefe-125">OU</span><span class="sxs-lookup"><span data-stu-id="7eefe-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="7eefe-126">**Obter Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="7eefe-127">**Atualizar Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="7eefe-128">**Excluir Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="7eefe-129">CRUDs de registro</span><span class="sxs-lookup"><span data-stu-id="7eefe-129">Registration CRUDs</span></span>
<span data-ttu-id="7eefe-130">**Crie um cliente do Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="7eefe-131">**Crie o registro do Windows:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="7eefe-132">**Crie registro do iOS:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="7eefe-133">Da mesma forma, você pode criar registros para Android (GCM), Windows Phone (MPNS) e Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="7eefe-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="7eefe-134">**Crie registros de modelo:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="7eefe-135">**Crie registros usando o padrão create registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="7eefe-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="7eefe-136">Remova duplicatas devido a todas as respostas perdidas se armazenar ids de registro no dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7eefe-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="7eefe-137">**Atualize os registros:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="7eefe-138">**Exclua os registros:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="7eefe-139">**Registros de consulta:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-139">**Query registrations:**</span></span>

* <span data-ttu-id="7eefe-140">**Obter um registro único:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="7eefe-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="7eefe-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="7eefe-142">**Obter todos os registros no hub:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="7eefe-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="7eefe-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="7eefe-144">**Obter registros com marca:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="7eefe-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="7eefe-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="7eefe-146">**Obter registros por canal:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="7eefe-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="7eefe-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="7eefe-148">Todas as consultas de coleção suportam tokens $top e de continuação.</span><span class="sxs-lookup"><span data-stu-id="7eefe-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="7eefe-149">Uso da API de instalação</span><span class="sxs-lookup"><span data-stu-id="7eefe-149">Installation API usage</span></span>
<span data-ttu-id="7eefe-150">A API de instalação é um mecanismo alternativo para gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="7eefe-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="7eefe-151">Em vez de manter vários registros, o que não é simples e pode ser feito incorretamente facilmente ou de maneira ineficiente, agora é possível usar um objeto de instalação ÚNICA.</span><span class="sxs-lookup"><span data-stu-id="7eefe-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span></span> <span data-ttu-id="7eefe-152">A instalação contém tudo o que você precisa: canal push (token de dispositivo), marcas, modelos, blocos secundários (para WNS e APNS).</span><span class="sxs-lookup"><span data-stu-id="7eefe-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="7eefe-153">Você não precisa mais chamar o serviço para obter o Id - apenas gerar GUID ou qualquer outro identificador, mantê-lo no dispositivo e enviar para o back-end com o canal push (token de dispositivo).</span><span class="sxs-lookup"><span data-stu-id="7eefe-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span></span> <span data-ttu-id="7eefe-154">No back-end, você deve fazer somente uma única chamada: CreateOrUpdateInstallation, ele é totalmente idempotente, então fique à vontade para tentar novamente se necessário.</span><span class="sxs-lookup"><span data-stu-id="7eefe-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span></span>

<span data-ttu-id="7eefe-155">Como exemplo, para o Amazon Kindle Fire ele tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="7eefe-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="7eefe-156">Se você quiser atualizá-lo:</span><span class="sxs-lookup"><span data-stu-id="7eefe-156">If you want to update it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="7eefe-157">Para cenários avançados, temos capacidade de atualização parcial, que lhe permite modificar apenas determinadas propriedades do objeto de instalação.</span><span class="sxs-lookup"><span data-stu-id="7eefe-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span></span> <span data-ttu-id="7eefe-158">Basicamente, a atualização parcial é o subconjunto de operações de Patch JSON, que você pode executar no objeto de instalação.</span><span class="sxs-lookup"><span data-stu-id="7eefe-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="7eefe-159">Excluir a instalação:</span><span class="sxs-lookup"><span data-stu-id="7eefe-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="7eefe-160">CreateOrUpdate, Patch e Delete são eventualmente consistentes com Get.</span><span class="sxs-lookup"><span data-stu-id="7eefe-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="7eefe-161">A operação solicitada só vai para a fila do sistema durante a chamada e será executada em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="7eefe-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span></span> <span data-ttu-id="7eefe-162">Observe que Get não foi projetado para o cenário principal do tempo de execução, mas apenas para depuração e solução de problemas, ele é totalmente restrito pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="7eefe-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span></span>

<span data-ttu-id="7eefe-163">Fluxo de envio para instalações é o mesmo para os registros.</span><span class="sxs-lookup"><span data-stu-id="7eefe-163">Send flow for Installations is the same as for Registrations.</span></span> <span data-ttu-id="7eefe-164">Acabamos de introduzir uma opção de notificação de destino para a instalação particular – basta usar a marca “InstallationId:{desired-id}".</span><span class="sxs-lookup"><span data-stu-id="7eefe-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="7eefe-165">Para o caso acima, ele ficaria assim:</span><span class="sxs-lookup"><span data-stu-id="7eefe-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="7eefe-166">Para um dos vários modelos:</span><span class="sxs-lookup"><span data-stu-id="7eefe-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="7eefe-167">Agendar notificações (disponível para a camada PADRÃO)</span><span class="sxs-lookup"><span data-stu-id="7eefe-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="7eefe-168">O mesmo que o envio regular, mas com um parâmetro adicional - scheduledTime que informa quando a notificação deve ser entregue.</span><span class="sxs-lookup"><span data-stu-id="7eefe-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="7eefe-169">O serviço aceita qualquer ponto de tempo entre agora + 5 minutos e agora + 7 dias.</span><span class="sxs-lookup"><span data-stu-id="7eefe-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="7eefe-170">**Agendar uma notificação nativa do Windows:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="7eefe-171">Importação/exportação (disponível para a camada PADRÃO)</span><span class="sxs-lookup"><span data-stu-id="7eefe-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="7eefe-172">Às vezes, é necessário para executar a operação em massa de registros.</span><span class="sxs-lookup"><span data-stu-id="7eefe-172">Sometimes it is required to perform bulk operation against registrations.</span></span> <span data-ttu-id="7eefe-173">Geralmente é para integração com outro sistema ou apenas uma correção maciça para confirmar a atualização das marcas.</span><span class="sxs-lookup"><span data-stu-id="7eefe-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span></span> <span data-ttu-id="7eefe-174">Altamente não é recomendável usar o fluxo de Get/Update se estivermos falando de milhares de registros.</span><span class="sxs-lookup"><span data-stu-id="7eefe-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="7eefe-175">O recurso de importação/exportação foi projetado para cobrir o cenário.</span><span class="sxs-lookup"><span data-stu-id="7eefe-175">Import/Export capability is designed to cover the scenario.</span></span> <span data-ttu-id="7eefe-176">Basicamente, fornecem um acesso a um contêiner de blob em sua conta de armazenamento como uma fonte de dados de entrada e local de saída.</span><span class="sxs-lookup"><span data-stu-id="7eefe-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="7eefe-177">**Envie o trabalho de exportação:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="7eefe-178">**Envie o trabalho de importação:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="7eefe-179">**Aguarde até que o trabalho seja feito:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="7eefe-180">**Obter todos os trabalhos:**</span><span class="sxs-lookup"><span data-stu-id="7eefe-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="7eefe-181">**URI com assinatura SAS:** esta é a URL de um arquivo de blob ou contêiner de blob mais o conjunto de parâmetros, como tempo de expiração e permissões mais assinatura de todas essas coisas feitas usando a chave SAS da conta.</span><span class="sxs-lookup"><span data-stu-id="7eefe-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="7eefe-182">O SDK Java do armazenamento do Azure tem recursos avançados, incluindo a criação de tal espécie de URIs.</span><span class="sxs-lookup"><span data-stu-id="7eefe-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="7eefe-183">Como alternativa simples, você pode dar uma olhada na classe de teste ImportExportE2E (a partir do local do github) que tem muitas implementações de algoritmo de assinatura básicas e compactas.</span><span class="sxs-lookup"><span data-stu-id="7eefe-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="7eefe-184">Enviar notificações</span><span class="sxs-lookup"><span data-stu-id="7eefe-184">Send Notifications</span></span>
<span data-ttu-id="7eefe-185">O objeto de notificação é simplesmente um corpo com cabeçalhos, alguns métodos de utilitário que ajudam na criação de objetos nativos e de modelo de notificações.</span><span class="sxs-lookup"><span data-stu-id="7eefe-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span></span>

* <span data-ttu-id="7eefe-186">**Windows Store e Windows Phone 8.1 (não Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="7eefe-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="7eefe-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="7eefe-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="7eefe-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="7eefe-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="7eefe-189">**Silverlight para Windows Phone 8.0 e 8.1**</span><span class="sxs-lookup"><span data-stu-id="7eefe-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="7eefe-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="7eefe-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="7eefe-191">**Enviar para Marcas**</span><span class="sxs-lookup"><span data-stu-id="7eefe-191">**Send to Tags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="7eefe-192">**Enviar a expressão de marca**</span><span class="sxs-lookup"><span data-stu-id="7eefe-192">**Send to tag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="7eefe-193">**Enviar notificação de modelo**</span><span class="sxs-lookup"><span data-stu-id="7eefe-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="7eefe-194">A execução do código Java agora deve produzir uma notificação que aparece no dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="7eefe-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="7eefe-195"><a name="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7eefe-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="7eefe-196">Neste tópico, mostramos como criar um cliente REST simples do Java para Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="7eefe-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="7eefe-197">A partir daqui, você pode:</span><span class="sxs-lookup"><span data-stu-id="7eefe-197">From here you can:</span></span>

* <span data-ttu-id="7eefe-198">Baixe o [SDK do Java]completo, que contém todo o código do SDK.</span><span class="sxs-lookup"><span data-stu-id="7eefe-198">Download the full [Java SDK], which contains the entire SDK code.</span></span> 
* <span data-ttu-id="7eefe-199">Brincar com os exemplos:</span><span class="sxs-lookup"><span data-stu-id="7eefe-199">Play with the samples:</span></span>
  * <span data-ttu-id="7eefe-200">[Introdução aos Hubs de Notificação]</span><span class="sxs-lookup"><span data-stu-id="7eefe-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="7eefe-201">[Enviar últimas notícias]</span><span class="sxs-lookup"><span data-stu-id="7eefe-201">[Send breaking news]</span></span>
  * <span data-ttu-id="7eefe-202">[Enviar últimas notícias localizadas]</span><span class="sxs-lookup"><span data-stu-id="7eefe-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="7eefe-203">[Enviar notificações aos usuários autenticados]</span><span class="sxs-lookup"><span data-stu-id="7eefe-203">[Send notifications to authenticated users]</span></span>
  * <span data-ttu-id="7eefe-204">[Enviar notificações entre plataformas aos usuários autenticados]</span><span class="sxs-lookup"><span data-stu-id="7eefe-204">[Send cross-platform notifications to authenticated users]</span></span>

<span data-ttu-id="7eefe-205">[SDK do Java]: https://github.com/Azure/azure-notificationhubs-java-backend</span><span class="sxs-lookup"><span data-stu-id="7eefe-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span></span>
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
<span data-ttu-id="7eefe-206">[Introdução aos Hubs de Notificação]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span><span class="sxs-lookup"><span data-stu-id="7eefe-206">[Get Started with Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span></span>
<span data-ttu-id="7eefe-207">[Enviar últimas notícias]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span><span class="sxs-lookup"><span data-stu-id="7eefe-207">[Send breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span></span>
<span data-ttu-id="7eefe-208">[Enviar últimas notícias localizadas]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="7eefe-208">[Send localized breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
<span data-ttu-id="7eefe-209">[Enviar notificações aos usuários autenticados]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span><span class="sxs-lookup"><span data-stu-id="7eefe-209">[Send notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span></span>
<span data-ttu-id="7eefe-210">[Enviar notificações entre plataformas aos usuários autenticados]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span><span class="sxs-lookup"><span data-stu-id="7eefe-210">[Send cross-platform notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span></span>
<span data-ttu-id="7eefe-211">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="7eefe-211">[Maven]: http://maven.apache.org/</span></span>

