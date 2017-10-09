## <a name="create-an-iot-hub"></a>Crie um hub IoT
Crie um hub IoT para sua tooconnect de aplicativo do dispositivo simulado para. Olá etapas a seguir mostram como toocomplete essa tarefa por usando Olá portal do Azure.

1. Entrar toohello [portal do Azure][lnk-portal].
1. No hello Jumpbar, clique em **novo** > **Internet das coisas** > **IoT Hub**.
   
    ![Barra de Navegação do portal do Azure][1]
1. Em Olá **hub IoT** folha, escolha a configuração Olá para o hub IoT.
   
    ![Folha Hub IoT][2]
   
   1. Em Olá **nome** , digite um nome para o hub IoT. Se hello **nome** é válido e disponível, uma marca de seleção verde é exibido no hello **nome** caixa.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Selecione um [tipo de preço e de dimensionamento][lnk-pricing]. Este tutorial não requer uma camada específica. Para este tutorial, use Olá F1 grátis.
   1. Em **Grupo de recursos**, crie um grupo de recursos ou selecione um existente. Para obter mais informações, consulte [usando o recurso de grupos de toomanage os recursos do Azure][lnk-resource-groups].
   1. Em **local**, selecione Olá local toohost seu hub IoT. Para este tutorial, escolha o local mais próximo.
1. Quando você tiver escolhido as opções de configuração do hub IoT, clique em **Criar**.  Pode levar alguns minutos para o Azure toocreate seu hub IoT. status de saudação toocheck, você pode monitorar o progresso de Olá Olá quadro inicial ou no painel de notificações de saudação.
   
    ![Novo status do Hub IoT do Azure][3]
1. Quando o hub IoT de saudação foi criado com êxito, clique em novo bloco Olá para o hub IoT na folha de Olá Olá tooopen portal do Azure para o hub IoT da nova hello. Anote Olá **Hostname**e, em seguida, clique em **políticas de acesso compartilhado**.
   
    ![Nova folha Hub IoT][4]
1. Em Olá **políticas de acesso compartilhado** folha, clique em Olá **iothubowner** política e, em seguida, copiar e anote Olá cadeia de caracteres de conexão de IoT Hub Olá **iothubowner** folha. Para obter mais informações, consulte [controle de acesso] [ lnk-access-control] em hello "Guia do desenvolvedor do IoT Hub."
   
    ![Folha Políticas de acesso compartilhado][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
