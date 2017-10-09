> [!div class="op_single_selector"]
> * [C em Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C em Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>Visão geral do cenário
Nesse cenário, você cria um dispositivo que envia Olá toohello telemetria de monitoramento remoto a seguir [pré-configurado solução][lnk-what-are-preconfig-solutions]:

* Temperatura externa
* Temperatura interna
* Umidade

Para simplificar, código de saudação no dispositivo hello gera valores de exemplo, mas recomendamos exemplo hello tooextend conectar sensores real tooyour dispositivo e enviar telemetria real.

dispositivo Olá também é capaz de toorespond toomethods invocada a partir do painel de solução de saudação e desejado valores de propriedade definidos no painel de solução de saudação.

toocomplete neste tutorial, você precisa de uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].

## <a name="before-you-start"></a>Antes de começar
Antes de escrever qualquer código para o seu dispositivo, você precisa provisionar a solução pré-configurada de monitoramento remoto e provisionar um novo dispositivo personalizado nessa solução.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Provisionar sua solução pré-configurada de monitoramento remoto
dispositivo Olá criado por você neste tutorial envia a instância de saudação tooan de dados [monitoramento remoto] [ lnk-remote-monitoring] pré-configurado de solução. Se você já não tiver provisionado Olá solução pré-configurada em sua conta do Azure de monitoramento remoto, use Olá etapas a seguir:

1. Em Olá <https://www.azureiotsuite.com/> , clique em  **+**  toocreate uma solução.
2. Clique em **selecione** em Olá **monitoramento remoto** painel toocreate sua solução.
3. Em hello **criar monitoramento remoto solução** , insira um **nome da solução** de sua escolha, selecione Olá **região** você deseja toodeploy para e selecione saudação do Azure assinatura toowant toouse. Clique em **Criar solução**.
4. Aguarde até que a saudação processo de provisionamento for concluído.

> [!WARNING]
> soluções de Olá pré-configurado usam os serviços do Azure faturáveis. Certifique-se de que tooremove Olá solução pré-configurada de sua assinatura, quando você tiver realizado tooavoid quaisquer encargos desnecessários. Você pode remover completamente uma solução pré-configurada de sua assinatura visitando Olá <https://www.azureiotsuite.com/> página.
> 
> 

Quando concluir a saudação processo para Olá remota de solução de monitoramento de provisionamento, clique em **iniciar** tooopen painel de solução de saudação em seu navegador.

![Painel da solução][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Configurar seu dispositivo no hello remota de solução de monitoramento
> [!NOTE]
> Se você já configurou um dispositivo em sua solução, poderá ignorar esta etapa. Você precisa ter credenciais de dispositivo de saudação do tooknow quando você cria o aplicativo de cliente hello.
> 
> 

Para uma solução de toohello pré-configurado de tooconnect do dispositivo, ele deve se identificar tooIoT Hub usando credenciais válidas. Você pode recuperar credenciais do dispositivo de saudação do painel de solução de saudação. Você pode incluir credenciais do dispositivo Olá em seu aplicativo cliente posteriormente neste tutorial.

tooadd uma solução de monitoramento remoto do tooyour dispositivo, Olá completo a seguir as etapas no painel de solução de saudação:

1. No hello canto inferior esquerdo do painel do hello, clique em **adicionar um dispositivo**.
   
   ![Adicionar um dispositivo][1]
2. Em Olá **dispositivo personalizado** do painel, clique em **adicionar novo**.
   
   ![Adicionar um dispositivo personalizado][2]
3. Escolha **Deixe-me definir minha própria ID de Dispositivo**. Insira uma ID de dispositivo como **meudispositivo**, clique em **verificar ID** tooverify esse nome não está em uso e, em seguida, clique em **criar** tooprovision dispositivo de saudação.
   
   ![Adicionar ID do dispositivo][3]
4. Tornar um dispositivo de saudação de Observação credenciais (ID do dispositivo, nome de host de Hub IoT e chave do dispositivo). Seu aplicativo cliente precisa de solução de monitoramento remoto toohello de tooconnect esses valores. Em seguida, clique em **Concluído**.
   
    ![Exibir credenciais do dispositivo][4]
5. Selecione o dispositivo na lista de dispositivos de saudação no painel de solução de saudação. Em seguida, no hello **detalhes do dispositivo** do painel, clique em **Ativar dispositivo**. status de saudação do seu dispositivo agora é **executando**. solução de monitoramento remoto Olá agora pode receber telemetria do seu dispositivo e chamar métodos no dispositivo de saudação.

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/