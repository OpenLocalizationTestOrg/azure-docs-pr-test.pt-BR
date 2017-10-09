## <a name="create-an-iot-hub"></a>Crie um hub IoT

1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **Internet das coisas** > **IoT Hub**.

   ![Criar um hub IoT em Olá portal do Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. Em Olá **hub IoT** painel, digite Olá informações para o hub IoT a seguir:

     **Nome**: Insira nome de saudação do seu hub IoT. Se o nome de saudação for válido, uma marca de seleção verde é exibida.

     **Escala e preço**: selecione Olá **F1 - livre** camada. Essa opção é suficiente para esta demonstração. Para obter mais informações, consulte Olá [camada de preços e escala](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Grupo de recursos**: criar um hub IoT de saudação do recurso grupo toohost ou use uma existente. Para obter mais informações, consulte [grupos de recurso de uso toomanage seus recursos do Azure](../articles/azure-resource-manager/resource-group-portal.md).

     **Local**: selecione Olá tooyou mais próximo do local em que o hub IoT de saudação é criado.

     **PIN toodashboard**: Selecione esta opção para o hub de IoT tooyour fácil acesso do painel de saudação.

   ![Insira informações toocreate seu hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Clique em **Criar**. O hub IoT levaria toocreate de alguns minutos. Você pode ver o progresso na Olá **notificações** painel.

   ![Ver as notificações de andamento para o hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. Depois que o hub IoT é criado, clique no painel de saudação. Anote Olá **Hostname**e, em seguida, clique em **políticas de acesso compartilhado**.

   ![Obter nome de host de saudação do seu hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. Em Olá **políticas de acesso compartilhado** painel, clique em Olá **iothubowner** política e, em seguida, copiar e anotado da saudação **cadeia de caracteres de Conexão** do seu hub IoT. Para obter mais informações, consulte [tooIoT de acesso de controle Hub](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
Você não precisará dessa cadeia de conexão iothubowner para este tutorial de configuração. No entanto, você pode precisar dele para alguns tutoriais Olá sobre diferentes cenários de IoT depois de concluir esta instalação.

   ![Obter sua cadeia de conexão do Hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Registrar um dispositivo no hub IoT de saudação do seu dispositivo

1. Em Olá [portal do Azure](https://portal.azure.com/), abra seu hub IoT.

2. Clique em **Gerenciador de Dispositivos**.
3. No painel de saudação do Gerenciador de dispositivos, clique em **adicionar** tooadd um hub do dispositivo tooyour IoT. Em seguida, Olá a seguir:

   **ID do dispositivo**: insira a ID de saudação do novo dispositivo de saudação. As IDs de Dispositivo diferenciam maiúsculas de minúsculas.

   **Tipo de Autenticação**: selecione a **Chave Simétrica**.

   **Gerar Chaves Automaticamente**: marque essa caixa de seleção.

   **Conecte-se o dispositivo tooIoT Hub**: clique em **habilitar**.

   ![Adicionar um dispositivo no hello Gerenciador de dispositivo de seu hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Clique em **Salvar**.
5. Após a criação de dispositivo hello, abrir o dispositivo de saudação em hello **dispositivo Explorer** painel.
6. Anote a chave primária Olá de cadeia de caracteres de conexão de saudação.

   ![Obter cadeia de caracteres de conexão de dispositivo Olá](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
