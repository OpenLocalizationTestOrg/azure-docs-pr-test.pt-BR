
# <a name="azure-and-internet-of-things"></a>Azure e Internet das Coisas

Bem-vindo tooMicrosoft do Azure e Olá Internet das coisas (IoT). Este artigo apresenta uma arquitetura de solução de IoT que descreve características comuns de saudação de uma solução de IoT, que você pode implantar usando os serviços do Azure. Soluções de IoT exigem a proteger a comunicação bidirecional entre os dispositivos, possivelmente numeração hello milhões e um back-end da solução. Por exemplo, um back-end da solução pode usar a análise automatizada e previsão toouncover insights de seu fluxo de eventos de dispositivo para nuvem.

O Hub IoT do Azure é um bloco de construção fundamental na implementação dessa arquitetura de solução de IoT usando os serviços do Azure. O IoT Suite fornece implementações completas de ponta a ponta dessa arquitetura para cenários específicos de IoT. Por exemplo:

* Olá *monitoramento remoto* solução permite que você toomonitor status de saudação de dispositivos como máquinas de vendas automáticas.
* Olá *manutenção preditiva* solução ajuda a tooanticipate necessidades de manutenção de dispositivos como bombas em estações bombeamento remotas e tempo de inatividade tooavoid agendada.
* Olá *fábrica conectada* solução ajuda a tooconnect e monitorar seus dispositivos industriais.

## <a name="iot-solution-architecture"></a>Arquitetura da solução de IoT

Olá diagrama a seguir mostra uma arquitetura de solução de IoT típica. diagrama de saudação não inclue nomes de saudação de todos os serviços do Azure específicos, mas descreve Olá principais elementos em uma arquitetura de solução de IoT genérico. Nessa arquitetura, dispositivos IoT coletam dados que enviam tooa gateway de nuvem. gateway de nuvem Olá disponibiliza Olá dados para processamento por outros serviços de back-end de onde os dados são entregues tooother aplicativos de linha de negócios ou operadores toohuman por meio de um painel ou outro dispositivo de apresentação.

![Arquitetura da solução de IoT][img-solution-architecture]

> [!NOTE]
> Para obter uma discussão detalhada da arquitetura do IoT, consulte Olá [arquitetura de referência do Microsoft Azure IoT][lnk-refarch].

### <a name="device-connectivity"></a>Conectividade do dispositivo

Nesta arquitetura de solução de IoT, dispositivos enviam telemetria, como leituras do sensor de uma estação bombeamento, tooa o ponto de extremidade de nuvem para armazenamento e processamento. Em um cenário de manutenção preditiva, back-end de solução Olá pode usar fluxo de saudação do sensor dados toodetermine quando uma bomba específica requer manutenção. Dispositivos também podem receber e responder mensagens toocloud para dispositivo lendo mensagens de um ponto de extremidade de nuvem. Por exemplo, na solução de Olá Olá manutenção preditiva cenário back-end pode enviar mensagens bombas tooother em Olá bombeamento estação toobegin redirecionamento fluxos antes de manutenção está vencida toostart. Esse procedimento seria Certifique-se de engenheiro de manutenção Olá pode começar assim que ela for recebida.

Um dos maiores desafios de saudação voltada para projetos de IoT é como tooreliably e se conectar com segurança dispositivos toohello solução back-end. Dispositivos IoT têm características diferentes, como clientes tooother comparados como navegadores e aplicativos móveis. Dispositivos IoT:

* Com frequência, são sistemas internos sem operadores humanos.
* Eles podem ser implantados em locais remotos, nos quais o acesso físico é caro.
* Só podem ser alcançadas por meio de back-end de solução hello. Não há nenhum outro toointeract maneira com dispositivo hello.
* Podem ter recursos de energia e de processamento limitados.
* Podem ter conectividade de rede intermitente, lenta ou cara.
* Talvez seja necessário toouse protocolos de aplicativo proprietárias, personalizados ou específicos do setor.
* Podem ser criados usando um grande conjunto de plataformas de hardware e de software conhecidas.

Além disso requisitos toohello acima, qualquer solução de IoT deve também fornecer dimensionamento, segurança e confiabilidade. Olá, conjunto de requisitos de conectividade resultante é difícil e demorado tooimplement usando tecnologias tradicionais como contêineres de web e os agentes de mensagens. IoT Hub do Azure e Olá SDKs de dispositivo IoT do Azure tornam mais fácil soluções tooimplement que atendem a esses requisitos.

Um dispositivo pode se comunicar diretamente com um ponto de extremidade de gateway de nuvem, ou se o dispositivo de saudação não é possível usar qualquer um dos protocolos de comunicação de saudação que Olá dá suporte ao gateway de nuvem, ele pode se conectar por meio de um gateway intermediário. Por exemplo, Olá [gateway do protocolo IoT do Azure] [ lnk-protocol-gateway] pode executar a conversão de protocolo se dispositivos não é possível usar qualquer um dos protocolos de saudação que dá suporte ao IoT Hub.

### <a name="data-processing-and-analytics"></a>Processamento de dados e análise

Na nuvem hello, um IoT solução back-end é onde ocorre a maior parte do processamento de dados de saudação, tais como filtragem e agregação de telemetria e roteá-la tooother serviços. Olá back-end de solução IoT:

* Recebe telemetria em escala de seus dispositivos e determina como tooprocess e armazenar os dados. 
* Poderá permitir que você toosend comandos de dispositivo de toospecific nuvem hello.
* Fornece recursos de registro de dispositivo que permitem que você tooprovision dispositivos e toocontrol quais dispositivos são permitidos tooconnect tooyour infraestrutura.
* Permite que você tootrack Olá estado de seus dispositivos e monitorar suas atividades.

No cenário de manutenção preditiva hello, back-end de solução Olá armazena dados de telemetria históricos. back-end de solução Olá pode usar este padrões tooidentify toouse de dados que indicam a manutenção ocorre em uma bomba específica.

As soluções de IoT podem incluir loops automáticos de comentários. Por exemplo, um módulo de análise no back-end de solução Olá pode identificar da telemetria temperatura Olá de um dispositivo específico está acima do normais níveis operacionais. solução de saudação pode enviar um dispositivo de toohello de comando, instruindo-tootake uma ação corretiva.

### <a name="presentation-and-business-connectivity"></a>Conectividade de negócios e apresentação

camada de conectividade de apresentação e de negócios Olá permite aos usuários finais toointeract com hello solução de IoT e dispositivos de saudação. Ele permite que os usuários tooview e analisar dados de saudação coletados em seus dispositivos. Esses modos de exibição podem assumir a forma de saudação de painéis ou relatórios de BI que podem exibir os dados históricos ou próximo a dados em tempo real. Por exemplo, um operador pode verificar status de saudação de estação bombeamento específica e ver todos os alertas gerados pelo sistema hello. Essa camada também permite que a integração de saudação IoT solução back-end com tootie de aplicativos de linha de negócios existentes em processos de negócios da empresa ou fluxos de trabalho. Por exemplo, solução de manutenção preditiva Olá pode integrar com um sistema de agendamento que manuais toovisit um engenheiro uma estação bombeamento quando a solução Olá identifica uma bomba que necessitam de manutenção.

![Painel da solução IoT][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
