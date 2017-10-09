## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você:

* Criar um aplicativo de console do Node. js que responde tooa método direto chamado pela nuvem Olá
* Disparar uma atualização de firmware simulada
* Olá Use relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles concluído pela última vez uma atualização de firmware

Etapa 1: crie uma pasta vazia denominada **manageddevice**.  Em Olá **manageddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```

Etapa 2: no prompt de comando no hello **manageddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** e **azure iot-dispositivo mqtt** dispositivo Pacotes do SDK:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Etapa 3: Usando um editor de texto, crie um **dmpatterns_fwupdate_device.js** arquivo hello **manageddevice** pasta.

Etapa 4: Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_fwupdate_device.js** arquivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Etapa 5: Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância. Substituir saudação `{yourdeviceconnectionstring}` espaço reservado com a cadeia de caracteres de conexão de saudação feitas anteriormente uma nota na seção "Criar uma identidade de dispositivo", Olá anteriormente:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Etapa 6: Adicionar a seguinte Olá função que é usado tooupdate relatado propriedades:
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

Etapa 7: Adicione Olá funções que simulam baixar e aplicar imagem do firmware Olá a seguir:
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

Etapa 8: Adicionar Olá após a função que o status de atualização de firmware atualizações Olá por meio de saudação relatados propriedades muito**esperando**. Normalmente, dispositivos serão informados sobre uma atualização disponível e um administrador definida política faz com que Olá dispositivo toostart baixar e aplicar atualização hello. Essa função é onde Olá tooenable lógica que política deve ser executado. Para simplificar, o exemplo hello aguarda quatro segundos antes de imagem do firmware continuar toodownload hello:
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

Etapa 9: Adicionar Olá após a função que o status de atualização de firmware atualizações Olá por meio de saudação relatados propriedades muito**download**. Olá função, em seguida, simula um download de firmware e finalmente atualizações Olá tooeither de status de atualização de firmware **downloadFailed** ou **downloadComplete**:
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

Etapa 10: Adicionar Olá após a função que o status de atualização de firmware atualizações Olá por meio de saudação relatados propriedades muito**aplicação**. Olá função, em seguida, simula aplicar imagem do firmware hello e finalmente atualizações Olá tooeither de status de atualização de firmware **applyFailed** ou **applyComplete**:
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

Etapa 11: Adicionar a função a seguir de Olá Olá que identificadores **firmwareUpdate** método direto e firmware de vários estágios Olá inicia o processo de atualização:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

Etapa 12: Finalmente, adicione Olá código que se conecta tooyour IoT hub a seguir:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 