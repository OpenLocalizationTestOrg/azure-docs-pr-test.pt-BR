## <a name="associate-an-azure-storage-account-tooiot-hub"></a>Associar uma conta de armazenamento do Azure tooIoT Hub

Como o aplicativo de dispositivo simulado Olá carrega um blob de tooa de arquivo, você deve ter uma [armazenamento do Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) tooIoT Hub associada à conta. Quando você associa uma conta de armazenamento do Azure com um hub IoT, o hub IoT de hello gera um URI de SAS. Um dispositivo pode usar esse carregamento do URI SAS toosecurely um contêiner de blob de tooa do arquivo. Olá serviço IoT Hub e hello SDKs do dispositivo coordenam processo Olá que gera Olá URI SAS e torna tooupload toouse de dispositivo disponível tooa um arquivo.

Siga as instruções de saudação em [uploads de arquivo de configuração usando Olá portal do Azure](../articles/iot-hub/iot-hub-configure-file-upload.md) tooassociate um hub IoT de tooyour de conta de armazenamento do Azure. Certifique-se de que um contêiner de blob é associado ao hub IoT e que as notificações de arquivo estão habilitadas.

![Habilitar Notificações de Arquivo no portal](media/iot-hub-associate-storage/enable-file-notifications.png)