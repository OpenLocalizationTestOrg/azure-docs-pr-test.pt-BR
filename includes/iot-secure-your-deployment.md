# <a name="secure-your-iot-deployment"></a>Proteger sua implantação de IoT
Este artigo fornece o próximo nível de detalhe de saudação para proteger a saudação infra-estrutura de IoT do Azure com base em Internet das coisas (IoT). Vincula tooimplementation detalhes de nível para configurar e implantar cada componente. Além disso, ele fornece comparações e opções entre vários métodos de concorrentes.

Protegendo a implantação do Azure IoT Olá pode ser dividido em Olá três áreas de segurança a seguir:

* **Segurança de dispositivo**: Protegendo dispositivo IoT de saudação enquanto ela está implantada em Olá curinga.
* **Segurança de Conexão**: verificar todos os dados transmitidos entre o dispositivo de IoT hello e IoT Hub é confidenciais e à prova de adulteração.
* **Segurança de nuvem**: fornecendo um meio toosecure dados enquanto se movimentam pelo e é armazenado na nuvem hello.

![Três áreas de segurança][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Provisionamento e autenticação com segurança dos dispositivos
Hello Azure IoT Suite protege dispositivos IoT por Olá dois métodos a seguir:

* Fornecendo uma chave de identidade exclusiva (tokens de segurança) para cada dispositivo, o que pode ser usado por Olá dispositivo toocommunicate com hello IoT Hub.
* Usando um dispositivo [certificado x. 509] [ lnk-x509] e a chave privada como um meio tooauthenticate Olá dispositivo toohello IoT Hub. Esse método de autenticação assegura que Olá chave privada no dispositivo de saudação não é conhecido fora dispositivo Olá a qualquer momento, fornecendo um nível mais alto de segurança.

método de token de segurança Hello fornece autenticação para cada chamada feita pelo Olá dispositivo tooIoT Hub por meio da associação chamada do hello tooeach chave simétrica. Autenticação baseada em x. 509 permite que a autenticação de um dispositivo IoT na camada física de Olá como parte do estabelecimento de conexão TLS hello. método de segurança baseada em token Hello pode ser usado sem a autenticação Olá x. 509 que é um padrão a menos segura. Hello escolha entre os métodos de saudação dois é principalmente ditada por Olá seguro como autenticação de dispositivo precisa toobe e a disponibilidade de armazenamento seguro no dispositivo de saudação (toostore Olá chave privada com segurança).

## <a name="iot-hub-security-tokens"></a>Tokens de segurança do Hub IoT
IoT Hub usa segurança tokens tooauthenticate dispositivos e serviços tooavoid enviar chaves na rede de saudação. Além disso, os tokens de segurança têm limite de escopo e de prazo de validade. Os SDKs do IoT do Azure geram automaticamente tokens sem precisar de configuração especial. Alguns cenários, no entanto, exigem Olá usuário toogenerate e usam tokens de segurança diretamente. Isso inclui o uso direto de saudação de superfícies MQTT, AMQP ou HTTP hello ou implementação de saudação do padrão do serviço de token de saudação.

Mais detalhes na estrutura de saudação do token de segurança hello e seu uso podem ser encontrados no hello artigos a seguir:

* [Estrutura do token de segurança][lnk-security-tokens]
* [Como usar tokens SAS como um dispositivo][lnk-sas-tokens]

Cada IoT Hub tem um [registro identidade] [ lnk-identity-registry] que pode ser usado toocreate por dispositivo recursos no serviço de saudação, como uma fila que contém mensagens de nuvem para dispositivo em andamento e tooallow toohello de acesso pontos de extremidade voltados para o dispositivo. Olá registro de identidade de IoT Hub fornece armazenamento seguro de identidades de dispositivo e chaves de segurança para uma solução. Individuais ou grupos de identidades do dispositivo podem ser adicionados tooan permitir lista ou uma lista de blocos, permitindo que o controle completo sobre o acesso ao dispositivo. Olá artigos a seguir fornecem mais detalhes na estrutura de saudação do registro de identidade hello e operações com suporte.

[O Hub IoT dá suporte a protocolos como HTTP, AMQP e MQTT][lnk-protocols]. Cada um desses protocolos usam tokens de segurança de tooIoT de dispositivo Olá IoT Hub maneiras diferentes:

* AMQP: Segurança de simples e baseada em declarações AMQP SASL ({policyName}@sas.root. { iothubName} no caso de saudação de tokens do nível do hub IoT; {deviceId} no caso de tokens no escopo do dispositivo).
* MQTT: Conectar usos do pacote {deviceId} como Olá {ClientId}, {IoThubhostname} / {deviceId} em Olá **Username** campo e um SAS de token em Olá **senha** campo.
* HTTP: Token válido está no cabeçalho de solicitação de autorização de saudação.

Registro de identidade de IoT Hub pode ser credenciais de segurança tooconfigure usado por dispositivo e controle de acesso. No entanto, se uma solução IoT já tiver um investimento considerável em um [Registro de identidade de dispositivo personalizado e/ou em um esquema de autenticação][lnk-custom-auth], ela poderá ser integrada a uma infraestrutura existente com o Hub IoT por meio da criação de um serviço de token.

### <a name="x509-certificate-based-device-authentication"></a>Autenticação de dispositivo com base no certificado x.509
Olá o uso de um [certificado baseado em dispositivo de x. 509] [ lnk-use-x509] e seu associado par de chaves pública e privada permite autenticação adicional na camada física hello. chave privada Olá é armazenada com segurança no dispositivo hello e não é detectável fora Olá dispositivo. certificado x. 509 de saudação contém informações sobre o dispositivo de saudação, como ID do dispositivo e outros detalhes organizacionais. Uma assinatura de certificado Olá é gerada usando a chave privada hello.

Fluxo de provisionamento do dispositivo de alto nível:

* Associe um identificador tooa dispositivo físico – identidade do dispositivo e/ou dispositivo de toohello associados de certificado x. 509 durante o dispositivo de fabricação ou preparação.
* Crie uma entrada de identidade correspondente no IoT Hub – dispositivo identidade e informações de dispositivo associado no Olá registro de identidade de IoT Hub.
* Armazene com segurança a impressão digital do certificado x.509 no Registro de identidade do Hub IoT.

### <a name="root-certificate-on-device"></a>Certificado raiz no dispositivo
Ao estabelecer uma conexão TLS segura com o IoT Hub, dispositivo de IoT Olá autentica IoT Hub usando um certificado raiz que é parte do dispositivo Olá SDK. Para SDK de cliente Olá C certificado Olá está localizado na pasta Olá "\\c\\certificados" na raiz de saudação do repositório de saudação. Embora esses certificados raiz são de vida longa, eles ainda podem expirar ou ser revogados. Se não houver nenhuma maneira de atualizar Olá certificado no dispositivo hello, hello dispositivo talvez não seja possível toosubsequently conectar toohello IoT Hub (ou qualquer outro serviço de nuvem). Ter um certificado de raiz significa tooupdate Olá depois que o dispositivo de IoT Olá é implantado será efetivamente reduzir esse risco.

## <a name="securing-hello-connection"></a>Protegendo a conexão Olá
Conexão de Internet entre o dispositivo de IoT hello e IoT Hub é protegida usando saudação padrão de segurança de camada de transporte (TLS). O Azure IoT dá suporte a [TLS 1.2][lnk-tls12], TLS 1.1 e TLS 1.0, nessa ordem. O suporte para TLS 1.0 é fornecido somente para fins de compatibilidade com versões anteriores. É recomendável toouse TLS 1.2 como ele fornece hello mais segurança.

Azure IoT Suite oferece suporte a saudação seguintes conjuntos de codificação, nessa ordem.

| Pacote de criptografia | Comprimento |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. RSA de 7680 bits) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. RSA de 3072 bits) FS |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. RSA de 7680 bits) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. RSA de 3072 bits) FS |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Proteção de nuvem Olá
O Hub IoT do Azure permite a definição de [políticas de controle de acesso][lnk-protocols] para cada chave de segurança. Ele usa Olá após o conjunto de permissões toogrant acesso tooeach de pontos de extremidade de IoT Hub. Permissões de limitam Olá acesso tooan que hub IoT é baseado na funcionalidade.

* **RegistryRead**. Registro de identidade de toohello do concede acesso de leitura. Para saber mais, consulte [Registro de identidade][lnk-identity-registry].
* **RegistryReadWrite**. Concede acesso de leitura e gravação toohello registro identidade. Para saber mais, consulte [Registro de identidade][lnk-identity-registry].
* **ServiceConnect**. Concede acesso toocloud serviço voltado para a comunicação e os pontos de extremidade de monitoramento. Por exemplo, ele concede mensagens de dispositivo para nuvem tooreceive do serviços de nuvem de tooback-end permissão, enviar mensagens de nuvem para dispositivo e recuperar Olá correspondente confirmações de entrega.
* **DeviceConnect**. Concede acesso toodevice voltados para pontos de extremidade. Por exemplo, ele concede permissão toosend mensagens de dispositivo para nuvem e receber mensagens de nuvem para dispositivo. Essa permissão é usada por dispositivos.

Há dois tooobtain de maneiras **DeviceConnect** permissões com o IoT Hub com [tokens de segurança][lnk-sas-tokens]: usando uma chave de identidade do dispositivo, ou uma chave de acesso compartilhado. Além disso, é importante toonote que toda a funcionalidade acessível a partir de dispositivos é exposta pelo design em pontos de extremidade com o prefixo `/devices/{deviceId}`.

[Componentes de serviço só podem gerar tokens de segurança] [ lnk-service-tokens] usando políticas de acesso concedendo permissões apropriadas hello.

IoT Hub do Azure e outros serviços que podem ser parte da solução Olá permitem o gerenciamento de usuários usando Olá Active Directory do Azure.

Dados ingeridos pelo Hub IoT do Azure podem ser consumidos por diversos serviços, como Stream Analytics do Azure e armazenamento de blobs do Azure. Esses serviços permitem o acesso de gerenciamento. Leia mais sobre esses serviços e opções disponíveis abaixo:

* [Documentos do Azure][lnk-docdb]: um serviço de banco de dados escalonáveis e totalmente indexados para dados estruturados que gerencia os metadados para dispositivos Olá provisionar, como atributos, configuração e propriedades de segurança. O DocumentDB oferece processamento de alto desempenho e alta taxa de transferência, indexação independente do esquema de dados e uma interface de consulta SQL avançada.
* [O Azure Stream Analytics][lnk-asa]: fluxo em tempo real de processamento na nuvem Olá que permite que você toorapidly desenvolver e implantar um baixo custo solução toouncover em tempo real resultados da análise dos dispositivos, sensores, infraestrutura e aplicativos. dados de saudação desse serviço totalmente gerenciado podem dimensionar tooany volume enquanto ainda atinge a resiliência, baixa latência e alta taxa de transferência.
* [Serviços de aplicativo do Azure][lnk-appservices]: uma nuvem plataforma toobuild avançados aplicativos web e móveis que se conectam toodata em qualquer lugar; na nuvem hello ou local. Compile aplicativos móveis atraentes para iOS, Android e Windows. Integre com o Software como um serviço (SaaS) e o enterprise aplicativos com conectividade de caixa toodozens de serviços baseados em nuvem e aplicativos corporativos. Código em seu idioma favorito e IDE (.NET, Node.js, PHP, Python ou Java) toobuild os aplicativos web e APIs mais rápido do que nunca.
* [Lógica de aplicativos][lnk-logicapps]: recurso de aplicativos lógicos de saudação do serviço de aplicativo do Azure ajuda a integrar seus sistemas de linha de negócios existentes do IoT solução tooyour e automatizar processos de fluxo de trabalho. Lógica de aplicativos permite que os desenvolvedores toodesign fluxos de trabalho Iniciar a partir de um gatilho e, em seguida, executam uma série de etapas, regras e ações que usam conectores poderoso toointegrate com seus processos de negócios. Lógica de aplicativos oferece um ecossistema de grande tooa fora da caixa de conectividade de SaaS, baseado em nuvem e aplicativos locais.
* [Armazenamento de BLOBs do Azure][lnk-blob]: armazenamento em nuvem confiável e econômica para dados de saudação seus dispositivos enviam toohello nuvem.

## <a name="conclusion"></a>Conclusão
Este artigo fornece uma visão geral dos detalhes de nível de implantação para projetar e implantar uma infraestrutura de IoT usando o Azure IoT. Configurar cada toobe componente seguro é chave proteger Olá infra-estrutura IoT geral. Opções de design Olá disponíveis no Azure IoT fornecerem algum nível de flexibilidade e a opção; No entanto, cada opção pode ter implicações de segurança. É recomendável que cada uma dessas opções seja avaliada por meio de uma avaliação de risco e custo.

[img-overview]: media/iot-secure-your-deployment/overview.png

[lnk-security-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../articles/iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-use-x509]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/
