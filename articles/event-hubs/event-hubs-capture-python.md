---
title: passo a passo aaaAzure Hubs de evento captura | Microsoft Docs
description: Exemplo que usa hello Azure SDK de Python toodemonstrate usando o recurso de captura de Hubs de evento hello.
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="48b72-103">Passo a passo da Captura de Hubs de Eventos: Python</span><span class="sxs-lookup"><span data-stu-id="48b72-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="48b72-104">Captura de Hubs de eventos é um recurso dos Hubs de eventos que permite que você tooautomatically entregar Olá fluxo de dados em seu hub de evento tooan conta de armazenamento de BLOBs do Azure de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="48b72-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="48b72-105">Esse recurso torna fácil tooperform processamento em lote em dados de streaming em tempo real.</span><span class="sxs-lookup"><span data-stu-id="48b72-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="48b72-106">Este artigo descreve como capturam de Hubs de eventos toouse com Python.</span><span class="sxs-lookup"><span data-stu-id="48b72-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="48b72-107">Para obter mais informações sobre captura de Hubs de evento, consulte Olá [artigo de visão geral](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48b72-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="48b72-108">Este exemplo usa Olá [Azure SDK de Python](https://azure.microsoft.com/develop/python/) toodemonstrate o recurso de captura hello.</span><span class="sxs-lookup"><span data-stu-id="48b72-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="48b72-109">programa de sender.py Olá envia telemetria ambiente simulada tooEvent Hubs no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="48b72-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="48b72-110">Olá hub de eventos está configurado toouse Olá captura recurso toowrite esse armazenamento tooblob de dados em lotes.</span><span class="sxs-lookup"><span data-stu-id="48b72-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="48b72-111">Olá capturereader.py aplicativo, em seguida, lê esses blobs e cria um arquivo de acrescentar por dispositivo e grava dados saudação em arquivos. csv.</span><span class="sxs-lookup"><span data-stu-id="48b72-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="48b72-112">O que será realizado</span><span class="sxs-lookup"><span data-stu-id="48b72-112">What will be accomplished</span></span>

1. <span data-ttu-id="48b72-113">Crie uma conta de armazenamento de BLOBs do Azure e um contêiner de blob dentro dele, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="48b72-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="48b72-114">Crie um namespace de Hub de eventos, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="48b72-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="48b72-115">Crie um hub de eventos com recurso de captura Olá habilitado, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="48b72-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="48b72-116">Envie um hub de eventos de toohello de dados com um script de Python.</span><span class="sxs-lookup"><span data-stu-id="48b72-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="48b72-117">Ler arquivos de saudação de captura hello e processá-los com outro script de Python.</span><span class="sxs-lookup"><span data-stu-id="48b72-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48b72-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="48b72-118">Prerequisites</span></span>

- <span data-ttu-id="48b72-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="48b72-119">Python 2.7.x</span></span>
- <span data-ttu-id="48b72-120">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="48b72-120">An Azure subscription</span></span>
- <span data-ttu-id="48b72-121">Um [Namespace de Hubs de Eventos e Hub de Eventos ativos.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="48b72-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="48b72-122">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="48b72-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="48b72-123">Faça logon no toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="48b72-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="48b72-124">No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, em seguida, clique em **armazenamento**e, em seguida, clique em **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="48b72-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="48b72-125">Preencha os campos de saudação na folha de conta de armazenamento hello e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="48b72-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="48b72-126">Depois de ver Olá **implantações bem-sucedida** , clique em nome de saudação da nova conta de armazenamento hello e em Olá **Essentials** folha, clique em **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="48b72-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="48b72-127">Olá quando **do serviço Blob** folha é aberto, clique em **+ contêiner** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="48b72-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="48b72-128">Contêiner de saudação do nome **capturar**, em seguida, feche Olá **do serviço Blob** folha.</span><span class="sxs-lookup"><span data-stu-id="48b72-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="48b72-129">Clique em **chaves de acesso** no hello esquerdo folha e cópia Olá o nome da conta de armazenamento hello e valor de saudação do **key1**.</span><span class="sxs-lookup"><span data-stu-id="48b72-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="48b72-130">Salve tooNotepad esses valores ou algum outro local temporário.</span><span class="sxs-lookup"><span data-stu-id="48b72-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="48b72-131">Criar um hub de eventos do Python script toosend eventos tooyour</span><span class="sxs-lookup"><span data-stu-id="48b72-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="48b72-132">Abra seu editor de Python favorito, como o [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="48b72-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="48b72-133">Crie um script chamado **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="48b72-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="48b72-134">Esse script envia 200 hub de eventos de tooyour de eventos.</span><span class="sxs-lookup"><span data-stu-id="48b72-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="48b72-135">Eles são simples leituras de ambiente enviadas em JSON.</span><span class="sxs-lookup"><span data-stu-id="48b72-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="48b72-136">Cole Olá código a seguir em sender.py:</span><span class="sxs-lookup"><span data-stu-id="48b72-136">Paste hello following code into sender.py:</span></span>
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. <span data-ttu-id="48b72-137">Atualize Olá anterior toouse de código, o nome do namespace, o valor da chave e o nome do hub de eventos que você obteve ao criar o namespace de Hubs de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="48b72-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="48b72-138">Criar um tooread de script de Python seus arquivos de captura</span><span class="sxs-lookup"><span data-stu-id="48b72-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="48b72-139">Preencha a folha de saudação e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="48b72-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="48b72-140">Criar um script chamado **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="48b72-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="48b72-141">Esse script lê Olá capturada arquivos e cria um arquivo de dados do dispositivo toowrite Olá por apenas para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="48b72-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="48b72-142">Cole Olá código a seguir em capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="48b72-142">Paste hello following code into capturereader.py:</span></span>
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. <span data-ttu-id="48b72-143">Ser toopaste-se de que os valores apropriados Olá para seu nome de conta de armazenamento e a chave no hello chamada muito`startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="48b72-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="48b72-144">Executar scripts de saudação</span><span class="sxs-lookup"><span data-stu-id="48b72-144">Run hello scripts</span></span>
1. <span data-ttu-id="48b72-145">Abra um prompt de comando com o Python em seu caminho e, em seguida, execute estes comandos tooinstall Python pré-requisitos do pacote:</span><span class="sxs-lookup"><span data-stu-id="48b72-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="48b72-146">Se você tiver uma versão anterior do armazenamento do azure ou do azure, talvez seja necessário Olá toouse **– atualizar** opção</span><span class="sxs-lookup"><span data-stu-id="48b72-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="48b72-147">Talvez também seja necessário toorun Olá seguir (não é necessária na maioria dos sistemas):</span><span class="sxs-lookup"><span data-stu-id="48b72-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="48b72-148">Alterar sua toowherever de diretório que você salvou sender.py e capturereader.py e execute este comando:</span><span class="sxs-lookup"><span data-stu-id="48b72-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="48b72-149">Esse comando inicia um novo remetente Python processo toorun hello.</span><span class="sxs-lookup"><span data-stu-id="48b72-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="48b72-150">Agora, aguarde alguns minutos para Olá captura toorun.</span><span class="sxs-lookup"><span data-stu-id="48b72-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="48b72-151">Em seguida, digite o comando a seguir em sua janela de comando original de saudação:</span><span class="sxs-lookup"><span data-stu-id="48b72-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="48b72-152">Este processador captura usa toodownload de diretório local Olá todos os blobs de saudação do contêiner da conta Olá armazenamento.</span><span class="sxs-lookup"><span data-stu-id="48b72-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="48b72-153">Ele processa qualquer um que não estejam vazias e grava os resultados de saudação como arquivos. csv no diretório local hello.</span><span class="sxs-lookup"><span data-stu-id="48b72-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48b72-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48b72-154">Next steps</span></span>

<span data-ttu-id="48b72-155">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="48b72-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="48b72-156">[Visão Geral da Captura de Hubs de Eventos][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="48b72-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="48b72-157">Um [aplicativo de exemplo completo que usa os Hubs de Eventos][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="48b72-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="48b72-158">Olá [expansão com Hubs de eventos de processamento de eventos] [ Scale out Event Processing with Event Hubs] exemplo.</span><span class="sxs-lookup"><span data-stu-id="48b72-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="48b72-159">[Visão Geral dos Hubs de Eventos][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="48b72-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
