## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8b7f5-101">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="8b7f5-101">Create a simulated device app</span></span>
<span data-ttu-id="8b7f5-102">Nesta seção, você:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-102">In this section, you:</span></span>

* <span data-ttu-id="8b7f5-103">Criar um aplicativo de console do Node. js que responde tooa método direto chamado pela nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="8b7f5-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="8b7f5-104">Disparar uma atualização de firmware simulada</span><span class="sxs-lookup"><span data-stu-id="8b7f5-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="8b7f5-105">Olá Use relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles concluído pela última vez uma atualização de firmware</span><span class="sxs-lookup"><span data-stu-id="8b7f5-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="8b7f5-106">Etapa 1: crie uma pasta vazia denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="8b7f5-107">Em Olá **manageddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="8b7f5-108">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="8b7f5-109">Etapa 2: no prompt de comando no hello **manageddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** e **azure iot-dispositivo mqtt** dispositivo Pacotes do SDK:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="8b7f5-110">Etapa 3: Usando um editor de texto, crie um **dmpatterns_fwupdate_device.js** arquivo hello **manageddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="8b7f5-111">Etapa 4: Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_fwupdate_device.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="8b7f5-112">Etapa 5: Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="8b7f5-113">Substituir saudação `{yourdeviceconnectionstring}` espaço reservado com a cadeia de caracteres de conexão de saudação feitas anteriormente uma nota na seção "Criar uma identidade de dispositivo", Olá anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="8b7f5-114">Etapa 6: Adicionar a seguinte Olá função que é usado tooupdate relatado propriedades:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
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

<span data-ttu-id="8b7f5-115">Etapa 7: Adicione Olá funções que simulam baixar e aplicar imagem do firmware Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
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

<span data-ttu-id="8b7f5-116">Etapa 8: Adicionar Olá após a função que o status de atualização de firmware atualizações Olá por meio de saudação relatados propriedades muito**esperando**.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="8b7f5-117">Normalmente, dispositivos serão informados sobre uma atualização disponível e um administrador definida política faz com que Olá dispositivo toostart baixar e aplicar atualização hello.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="8b7f5-118">Essa função é onde Olá tooenable lógica que política deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="8b7f5-119">Para simplificar, o exemplo hello aguarda quatro segundos antes de imagem do firmware continuar toodownload hello:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
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

<span data-ttu-id="8b7f5-120">Etapa 9: Adicionar Olá após a função que o status de atualização de firmware atualizações Olá por meio de saudação relatados propriedades muito**download**.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="8b7f5-121">Olá função, em seguida, simula um download de firmware e finalmente atualizações Olá tooeither de status de atualização de firmware **downloadFailed** ou **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="8b7f5-122">Etapa 10: Adicionar Olá após a função que o status de atualização de firmware atualizações Olá por meio de saudação relatados propriedades muito**aplicação**.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="8b7f5-123">Olá função, em seguida, simula aplicar imagem do firmware hello e finalmente atualizações Olá tooeither de status de atualização de firmware **applyFailed** ou **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="8b7f5-124">Etapa 11: Adicionar a função a seguir de Olá Olá que identificadores **firmwareUpdate** método direto e firmware de vários estágios Olá inicia o processo de atualização:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="8b7f5-125">Etapa 12: Finalmente, adicione Olá código que se conecta tooyour IoT hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b7f5-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
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
> <span data-ttu-id="8b7f5-126">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="8b7f5-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8b7f5-127">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b7f5-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 