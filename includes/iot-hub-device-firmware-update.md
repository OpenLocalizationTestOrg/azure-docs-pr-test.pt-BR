## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c398c-101">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="c398c-101">Create a simulated device app</span></span>
<span data-ttu-id="c398c-102">Nesta seção, você:</span><span class="sxs-lookup"><span data-stu-id="c398c-102">In this section, you:</span></span>

* <span data-ttu-id="c398c-103">Criar um aplicativo de console do Node.js que responde a um método direto chamado pela nuvem</span><span class="sxs-lookup"><span data-stu-id="c398c-103">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="c398c-104">Disparar uma atualização de firmware simulada</span><span class="sxs-lookup"><span data-stu-id="c398c-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="c398c-105">Usar as propriedades relatadas para habilitar consultas de dispositivo gêmeo para identificar dispositivos e quando foi a última atualização de firmware concluída</span><span class="sxs-lookup"><span data-stu-id="c398c-105">Use the reported properties to enable device twin queries to identify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="c398c-106">Etapa 1: crie uma pasta vazia denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="c398c-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="c398c-107">Na pasta **manageddevice**, crie um arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="c398c-107">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="c398c-108">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="c398c-108">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="c398c-109">Etapa 2: no prompt de comando na pasta **manageddevice**, execute o seguinte comando para instalar os pacotes **azure-iot-device** e **azure-iot-device-mqtt** do SDK do Dispositivo:</span><span class="sxs-lookup"><span data-stu-id="c398c-109">Step 2: At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="c398c-110">Etapa 3: usando um editor de texto, crie um arquivo **dmpatterns_fwupdate_device.js** na pasta **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="c398c-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in the **manageddevice** folder.</span></span>

<span data-ttu-id="c398c-111">Etapa 4: adicione as seguintes instruções "require" no início do arquivo **dmpatterns_fwupdate_device.js**:</span><span class="sxs-lookup"><span data-stu-id="c398c-111">Step 4: Add the following 'require' statements at the start of the **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="c398c-112">Etapa 5: adicione uma variável **connectionString** e use-a para criar uma instância **Cliente**.</span><span class="sxs-lookup"><span data-stu-id="c398c-112">Step 5: Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="c398c-113">Substitua o `{yourdeviceconnectionstring}` espaço reservado com a cadeia de conexão que você anotou na seção "Criar uma identidade de dispositivo" anteriormente:</span><span class="sxs-lookup"><span data-stu-id="c398c-113">Replace the `{yourdeviceconnectionstring}` placeholder with the connection string you previously made a note of in the "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="c398c-114">Etapa 6: adicione a seguinte função, que será usada para atualizar as propriedades relatadas:</span><span class="sxs-lookup"><span data-stu-id="c398c-114">Step 6: Add the following function that is used to update reported properties:</span></span>
   
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

<span data-ttu-id="c398c-115">Etapa 7: adicione as seguintes funções que simulam baixar e aplicar a imagem do firmware:</span><span class="sxs-lookup"><span data-stu-id="c398c-115">Step 7: Add the following functions that simulate downloading and applying the firmware image:</span></span>
   
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

<span data-ttu-id="c398c-116">Etapa 8: adicione a seguinte função, que atualizará o status da atualização de firmware por meio das propriedades relatadas para **aguardando**.</span><span class="sxs-lookup"><span data-stu-id="c398c-116">Step 8: Add the following function that updates the firmware update status through the reported properties to **waiting**.</span></span> <span data-ttu-id="c398c-117">Normalmente, os dispositivos serão informados sobre uma atualização disponível e uma política definida pelo administrador fará com que o dispositivo inicie o download e aplique a atualização.</span><span class="sxs-lookup"><span data-stu-id="c398c-117">Typically, devices are informed of an available update and an administrator defined policy causes the device to start downloading and applying the update.</span></span> <span data-ttu-id="c398c-118">Essa função é onde a lógica para habilitar essa política deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="c398c-118">This function is where the logic to enable that policy should run.</span></span> <span data-ttu-id="c398c-119">Para simplificar, o exemplo aguarda quatro segundos antes de continuar a baixar a imagem do firmware:</span><span class="sxs-lookup"><span data-stu-id="c398c-119">For simplicity, the sample waits for four seconds before proceeding to download the firmware image:</span></span>
   
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

<span data-ttu-id="c398c-120">Etapa 9: adicione a seguinte função, que atualizará o status da atualização de firmware por meio das propriedades relatadas para **baixando**.</span><span class="sxs-lookup"><span data-stu-id="c398c-120">Step 9: Add the following function that updates the firmware update status through the reported properties to **downloading**.</span></span> <span data-ttu-id="c398c-121">A função, em seguida, simula um download de firmware e finalmente atualiza o status de atualização do firmware para o **downloadFailed** ou **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="c398c-121">The function then simulates a firmware download and finally updates the firmware update status to either **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="c398c-122">Etapa 10: adicione a seguinte função, que atualizará o status da atualização de firmware por meio das propriedades relatadas para **aplicando**.</span><span class="sxs-lookup"><span data-stu-id="c398c-122">Step 10: Add the following function that updates the firmware update status through the reported properties to **applying**.</span></span> <span data-ttu-id="c398c-123">A função simula a aplicação da imagem de firmware e finalmente atualiza o status de atualização do firmware para o **applyFailed** ou **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="c398c-123">The function then simulates applying the firmware image and finally updates the firmware update status to either **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="c398c-124">Etapa 11: adicione a seguinte função que manipula o método direto **firmwareUpdate** e inicia a atualização de firmware de vários estágios de processo:</span><span class="sxs-lookup"><span data-stu-id="c398c-124">Step 11: Add the following function that handles the **firmwareUpdate** direct method and initiates the multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond the cloud app for the direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response to method \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get the parameter from the body of the method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain the device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start the multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="c398c-125">Etapa 12: finalmente, adicione o seguinte código que se conecta ao seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="c398c-125">Step 12: Finally, add the following code that connects to your IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect to IotHub client');
      }  else {
        console.log('Client connected to IoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="c398c-126">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="c398c-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c398c-127">No código de produção, implemente políticas de repetição (como uma retirada exponencial), conforme sugerido no artigo [Tratamento de falhas transitórias](https://msdn.microsoft.com/library/hh675232.aspx) do MSDN.</span><span class="sxs-lookup"><span data-stu-id="c398c-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 