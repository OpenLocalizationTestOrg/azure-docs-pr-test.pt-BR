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
# <a name="event-hubs-capture-walkthrough-python"></a>Passo a passo da Captura de Hubs de Eventos: Python

Captura de Hubs de eventos é um recurso dos Hubs de eventos que permite que você tooautomatically entregar Olá fluxo de dados em seu hub de evento tooan conta de armazenamento de BLOBs do Azure de sua escolha. Esse recurso torna fácil tooperform processamento em lote em dados de streaming em tempo real. Este artigo descreve como capturam de Hubs de eventos toouse com Python. Para obter mais informações sobre captura de Hubs de evento, consulte Olá [artigo de visão geral](event-hubs-archive-overview.md).

Este exemplo usa Olá [Azure SDK de Python](https://azure.microsoft.com/develop/python/) toodemonstrate o recurso de captura hello. programa de sender.py Olá envia telemetria ambiente simulada tooEvent Hubs no formato JSON. Olá hub de eventos está configurado toouse Olá captura recurso toowrite esse armazenamento tooblob de dados em lotes. Olá capturereader.py aplicativo, em seguida, lê esses blobs e cria um arquivo de acrescentar por dispositivo e grava dados saudação em arquivos. csv.

## <a name="what-will-be-accomplished"></a>O que será realizado

1. Crie uma conta de armazenamento de BLOBs do Azure e um contêiner de blob dentro dele, usando Olá portal do Azure.
2. Crie um namespace de Hub de eventos, usando Olá portal do Azure.
3. Crie um hub de eventos com recurso de captura Olá habilitado, usando Olá portal do Azure.
4. Envie um hub de eventos de toohello de dados com um script de Python.
5. Ler arquivos de saudação de captura hello e processá-los com outro script de Python.

## <a name="prerequisites"></a>Pré-requisitos

- Python 2.7.x
- Uma assinatura do Azure
- Um [Namespace de Hubs de Eventos e Hub de Eventos ativos.](event-hubs-create.md)

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Criar uma conta de Armazenamento do Azure
1. Faça logon no toohello [portal do Azure][Azure portal].
2. No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, em seguida, clique em **armazenamento**e, em seguida, clique em **conta de armazenamento**.
3. Preencha os campos de saudação na folha de conta de armazenamento hello e, em seguida, clique em **criar**.
   
   ![][1]
4. Depois de ver Olá **implantações bem-sucedida** , clique em nome de saudação da nova conta de armazenamento hello e em Olá **Essentials** folha, clique em **Blobs**. Olá quando **do serviço Blob** folha é aberto, clique em **+ contêiner** na parte superior da saudação. Contêiner de saudação do nome **capturar**, em seguida, feche Olá **do serviço Blob** folha.
5. Clique em **chaves de acesso** no hello esquerdo folha e cópia Olá o nome da conta de armazenamento hello e valor de saudação do **key1**. Salve tooNotepad esses valores ou algum outro local temporário.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Criar um hub de eventos do Python script toosend eventos tooyour
1. Abra seu editor de Python favorito, como o [Visual Studio Code][Visual Studio Code].
2. Crie um script chamado **sender.py**. Esse script envia 200 hub de eventos de tooyour de eventos. Eles são simples leituras de ambiente enviadas em JSON.
3. Cole Olá código a seguir em sender.py:
   
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
4. Atualize Olá anterior toouse de código, o nome do namespace, o valor da chave e o nome do hub de eventos que você obteve ao criar o namespace de Hubs de eventos de saudação.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Criar um tooread de script de Python seus arquivos de captura

1. Preencha a folha de saudação e clique em **criar**.
2. Criar um script chamado **capturereader.py**. Esse script lê Olá capturada arquivos e cria um arquivo de dados do dispositivo toowrite Olá por apenas para o dispositivo.
3. Cole Olá código a seguir em capturereader.py:
   
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
4. Ser toopaste-se de que os valores apropriados Olá para seu nome de conta de armazenamento e a chave no hello chamada muito`startProcessing`.

## <a name="run-hello-scripts"></a>Executar scripts de saudação
1. Abra um prompt de comando com o Python em seu caminho e, em seguida, execute estes comandos tooinstall Python pré-requisitos do pacote:
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Se você tiver uma versão anterior do armazenamento do azure ou do azure, talvez seja necessário Olá toouse **– atualizar** opção
   
  Talvez também seja necessário toorun Olá seguir (não é necessária na maioria dos sistemas):
   
  ```
  pip install cryptography
  ```
2. Alterar sua toowherever de diretório que você salvou sender.py e capturereader.py e execute este comando:
   
  ```
  start python sender.py
  ```
   
  Esse comando inicia um novo remetente Python processo toorun hello.
3. Agora, aguarde alguns minutos para Olá captura toorun. Em seguida, digite o comando a seguir em sua janela de comando original de saudação:
   
   ```
   python capturereader.py
   ```

   Este processador captura usa toodownload de diretório local Olá todos os blobs de saudação do contêiner da conta Olá armazenamento. Ele processa qualquer um que não estejam vazias e grava os resultados de saudação como arquivos. csv no diretório local hello.

## <a name="next-steps"></a>Próximas etapas

Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral da Captura de Hubs de Eventos][Overview of Event Hubs Capture]
* Um [aplicativo de exemplo completo que usa os Hubs de Eventos][sample application that uses Event Hubs].
* Olá [expansão com Hubs de eventos de processamento de eventos] [ Scale out Event Processing with Event Hubs] exemplo.
* [Visão Geral dos Hubs de Eventos][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
