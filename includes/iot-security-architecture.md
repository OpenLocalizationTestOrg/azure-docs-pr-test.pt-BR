# <a name="internet-of-things-security-architecture"></a>Arquitetura de segurança da Internet das Coisas
Durante a criação de um sistema, é importante toounderstand ameaças em potencial Olá toothat sistema e adicionar defesas apropriadas da mesma forma, como sistema de saudação é desenvolvido e projetado. É particularmente importante toodesign Olá produto a partir do início da saudação pensando na segurança porque a entender como um invasor pode ser capaz de toocompromise um sistema de ajuda a certificar-se de que as atenuações apropriadas estejam no local de início de saudação. 

## <a name="security-starts-with-a-threat-model"></a>A segurança começa com um modelo de risco
Microsoft tempo tenha usado modelos de risco para seus produtos e fez publicamente disponíveis do processo de modelagem de ameaças da empresa hello. Olá experiência da empresa demonstra que Olá modelagem tem benefícios inesperados além Olá imediata compreender quais ameaças são Olá relacionados com a maioria dos. Por exemplo, ele também cria um canal para uma discussão aberta com outras pessoas fora da equipe de desenvolvimento hello, que pode levar toonew ideias e aprimoramentos no produto hello.

objetivo de saudação da modelagem de ameaças é toounderstand como um invasor pode ser capaz de toocompromise um sistema e, em seguida, certifique-se de atenuações apropriadas estejam em vigor. Modelagem de ameaças força reduções de tooconsider de equipe de design hello como Olá sistema foi projetado em vez de após a implantação de um sistema. Esse fato é extremamente importante, porque o aperfeiçoamento uma infinidade de tooa de defesas de segurança de dispositivos em campo Olá for inviável, sujeito a erros e deixará os clientes em risco.

Muitas equipes de desenvolvimento fazem um excelente trabalho de captura Olá funcional os requisitos do sistema Olá que beneficiam os clientes. No entanto, a identificar maneiras não óbvio que alguém pode usar indevidamente sistema Olá é mais difícil. A modelagem de risco pode ajudar as equipes de desenvolvimento a compreender o que um invasor pode fazer e por quê. Modelagem de ameaças é um processo estruturado que cria uma discussão sobre segurança Olá decisões de design no sistema hello, bem como o design de toohello as alterações feitas ao longo de maneira Olá que afetam a segurança. Enquanto um modelo de ameaça é simplesmente um documento, esta documentação também representa uma maneira ideal de continuidade de tooensure de Conhecimento, retenção de lições aprendidas e ajudar a nova equipe integrar rapidamente. Por fim, um resultado de modelagem de ameaças é tooenable tooconsider você outros aspectos de segurança, como quais os compromissos de segurança você deseja tooprovide tooyour clientes. Esses compromissos em conjunto com a modelagem de risco informarão e orientarão o teste de sua solução de IoT (Internet das Coisas).

### <a name="when-toothreat-model"></a>Quando o modelo de toothreat
[Modelagem de ameaças](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) ofertas Olá maior valor se ele é incorporado na fase de design de saudação. Quando você está criando, você tem Olá maior flexibilidade toomake alterações tooeliminate ameaças. Eliminar ameaças por design é o resultado desejado hello. É muito mais fácil do que adicionar mitigações, testá-las e garantir que elas permaneçam atualizadas e, além disso, essa eliminação nem sempre é possível. Ele se torna mais difícil tooeliminate ameaças como um produto se torna mais maduros e por sua vez, por fim, exigirá mais trabalho e muito mais difícil compensações de modelagem desde o início do desenvolvimento de saudação de ameaça.

### <a name="what-toothreat-model"></a>O modelo de toothreat
Você deve thread solução de saudação do modelo como um todo e também o foco no hello áreas a seguir:

* recursos de segurança e privacidade Olá
* recursos de saudação cujas falhas são relevantes de segurança
* recursos de saudação que tocam um limite de confiança 

### <a name="who-threat-models"></a>Quem faz os modelos de risco
A modelagem de risco é um processo como qualquer outro.  É um documento de modelo de ameaça do BOM tootreat hello como qualquer outro componente de solução de saudação e validá-lo. Muitas equipes de desenvolvimento fazem um excelente trabalho de captura Olá funcional os requisitos do sistema Olá que beneficiam os clientes. No entanto, a identificar maneiras não óbvio que alguém pode usar indevidamente sistema Olá é mais difícil. A modelagem de risco pode ajudar as equipes de desenvolvimento a compreender o que um invasor pode fazer e por quê.

### <a name="how-toothreat-model"></a>Como o modelo de toothreat
processo de modelagem de ameaças Olá é composta de quatro etapas; Olá etapas são:

* Aplicativo hello modelo
* Enumerar as ameaças
* Atenuar as ameaças
* Validar atenuações Olá

#### <a name="hello-process-steps"></a>etapas do processo Olá
Tookeep três princípios em mente ao criar um modelo de ameaça:

1. Crie um diagrama da arquitetura de referência. 
2. Inicie primeiro por abrangência. Obtenha uma visão geral e entender o sistema hello como um todo, antes de se aprofundar profundo.  Isso ajuda a garantir que você aprofundar em Olá direita coloca.
3. Unidade processo hello, não permitem que o processo de saudação unidade você. Se você encontrar um problema na fase de modelagem de saudação e deseja tooexplore-lo, vá para ele!  Não precisarão toofollow essas etapas submissamente.  

#### <a name="threats"></a>Ameaças
Olá quatro principais elementos de um modelo de ameaça são:

* Processos (serviços Web, serviços do Win32, daemons *nix etc.) Observe que algumas entidades complexas (por exemplo, gateways de campo e sensores) podem ser abstraídas como um processo quando um detalhamento técnico nessas áreas não é possível.
* Armazenamentos de dados (qualquer lugar em que os dados são armazenados, como um arquivo de configuração ou banco de dados)
* Fluxo de dados (onde dados se movimentarem entre outros elementos no aplicativo hello)
* Entidades externas (qualquer coisa que interage com o sistema hello, mas não é controlada saudação do aplicativo hello, os exemplos incluem usuários e feeds de satélite)

Todos os elementos no diagrama de arquitetura de saudação são ameaças de toovarious assunto; usaremos mnemônico STRIDE hello. Leitura [Threat Modeling novamente, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow mais sobre os elementos STRIDE hello.

Elementos de diagrama do aplicativo hello são ameaças STRIDE toocertain assunto:

* Os processos são tooSTRIDE de assunto
* Fluxos de dados são o assunto tooTID
* Armazenamentos de dados são tooTID de assunto e, às vezes, R, se Olá armazenamentos de dados são arquivos de log.
* Entidades externas são tooSRD de assunto

## <a name="security-in-iot"></a>Segurança na IoT
Dispositivos conectados de finalidade especial tem um número significativo de áreas da superfície potencial interação e padrões de interação, que deve ser considerado tooprovide uma estrutura para proteger o acesso digital toothose dispositivos. termo Hello "digital access" é usado toodistinguish aqui de todas as operações que são executadas por meio da interação direta do dispositivo onde a segurança de acesso é fornecida por meio do controle de acesso físico. Por exemplo, colocando dispositivo Olá em uma sala com um bloqueio na porta hello. Enquanto o acesso físico não pode ser negado usando hardware e software, medidas podem ser tomadas tooprevent o acesso físico dos principais toosystem interferência. 

Como podemos explorar os padrões de interação de hello, examinaremos "controle de dispositivo" e "dados de dispositivo" com o mesmo nível de atenção de hello. "Controle de dispositivo" pode ser classificado como qualquer informação fornecida tooa dispositivo por qualquer pessoa com objetivo de saudação de alteração ou influenciar o comportamento para seu estado ou saudação do seu ambiente. "Dados de dispositivo" podem ser classificados como todas as informações que um dispositivo emite tooany outro participante sobre seu estado e Olá observado o estado do seu ambiente.

Em ordem toooptimize práticas recomendadas, é recomendável que uma arquitetura típica do IoT ser divididos em várias/zonas de componente como parte do exercício de modelagem de ameaças de saudação. Essas zonas são descritas em detalhes ao longo desta seção e incluem:

* Dispositivo,
* Gateway de campo,
* Gateways de nuvem e
* .

As zonas são amplo toosegment de maneira uma solução; Geralmente, cada região tem seus próprios requisitos de dados e autenticação e autorização. As zonas também podem ser usado tooisolation danos e restringir o impacto de saudação das zonas de confiança baixa em zonas de confiança superior.

Cada zona é separada por um limite de confiança é indicado como Olá linhas pontilhadas linha vermelha no diagrama de saudação abaixo. Representa uma transição de informações/dados de uma fonte tooanother. Durante essa transição, informações da dados Olá pode ser tooSpoofing de assunto, violação, repúdio, divulgação de informações, negação de serviço e elevação de privilégio (STRIDE).

![Zonas de segurança da IoT](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Olá componentes descritos em cada limite também são tooSTRIDE sujeito, habilitando um 360 completo exibição de solução de saudação de modelagem de ameaças. seções de saudação abaixo elaborem em cada um dos componentes de saudação e questões de segurança específico e soluções que devem ser colocadas em prática.

seções Olá após discutir componentes padrão geralmente encontrado nessas zonas.

### <a name="hello-device-zone"></a>Olá fuso do dispositivo
Olá, ambiente do dispositivo é espaço físico do imediato saudação dispositivo Olá onde o acesso físico e/ou digital de ponto a ponto "rede local" acessar toohello dispositivo é viável. "Rede local" é assumida toobe uma rede que é distinto e isolamento de – mas potencialmente ligados com pontes Internet pública muito – hello e inclui qualquer tecnologia de rádio de curta distância que permite a comunicação ponto a ponto de dispositivos. Ele faz *não* incluem qualquer tecnologia de virtualização de rede criando ilusão Olá dessa rede local e também não incluir redes de operador público que necessitam de quaisquer dois dispositivos toocommunicate em espaço de rede pública Se eles fossem relação de comunicação tooenter uma ponto a ponto.

### <a name="hello-field-gateway-zone"></a>Olá campo Gateway de zona
Um gateway de campo é um dispositivo ou um software de computador servidor de finalidade geral que age como um habilitador de comunicação e, potencialmente, como um sistema de controle de dispositivo e um hub de processamento de dados do dispositivo. zona de gateway de campo Olá inclui o próprio gateway de campo hello e todos os dispositivos que estão anexados tooit. Como Olá nome implica, gateways de campo agir instalações fora de processamento de dados dedicado, são geralmente local associado, é potencialmente invasão de toophysical de assunto e terão redundância operacional. Todos os toosay que um gateway de campo geralmente é uma coisa um pode toque e sabotar sabendo sua função é. 

Um gateway de campo é diferente de um mero roteador de tráfego em que ele teve uma função ativa no gerenciamento de acesso e fluxo de informações, o que significa que ele é um terminal de sessão ou uma conexão de rede e entidade dirigida para o aplicativo. Um firewall ou dispositivos NAT, por outro lado, não se qualificam como gateways de campo, pois não são terminais de sessão ou conexão explícitos, mas sim sessões ou conexões de rota (ou bloqueio) feitas por meio deles. gateway de campo Olá tem duas áreas da superfície distintas. Um faces dispositivos Olá tooit anexado e representa hello dentro de zona hello e Olá outros fica disponível para todos os parceiros externos e Olá borda da zona de saudação.   

### <a name="hello-cloud-gateway-zone"></a>zona de gateway de nuvem Olá
Gateway de nuvem é um sistema que permite a comunicação remota do e gateways toodevices ou campo de diversos sites em espaço de rede pública, normalmente até um baseado em nuvem controle e dados de sistema de análise, uma federação de tais sistemas. Em alguns casos, um gateway de nuvem pode facilitar imediatamente acessem dispositivos de toospecial com a finalidade de terminais, como tablets e telefones. No contexto de saudação discutido aqui, "nuvem" destina toorefer tooa dedicado processamento de dados de sistema que não esteja associado toohello mesmo site como Olá anexado dispositivos ou gateways de campo. Também em uma região de nuvem, medidas operacionais impedem o acesso físico de destino em não é necessariamente exposto tooa infra-estrutura de "nuvem pública".  

Um gateway de nuvem potencialmente pode ser mapeado para um gateway de rede virtualização sobreposição tooinsulate Olá nuvem e todos os seus dispositivos anexados ou gateways de campo de qualquer outro tráfego de rede. gateway de nuvem Olá em si não é um sistema de controle de dispositivo nem um processamento ou depósito de dados do dispositivo; Esses recursos de interajam com o gateway de nuvem hello. zona de gateway de nuvem de saudação inclui Olá nuvem próprio gateway junto com todos os gateways de campo e dispositivos direta ou indiretamente conectado tooit. borda de saudação da zona de saudação é uma área de superfície distinta onde todos os parceiros externos se comunicam através de.

### <a name="hello-services-zone"></a>zona de serviços Olá
Um "serviço" é definido para este contexto como qualquer componente de software ou módulo que faz interface com dispositivos através de um gateway de nuvem ou campo para coleta e análise de dados, bem como para o comando e controle.  Os serviços são mediadores. Atuar em sua identidade com relação a gateways e outros subsistemas, armazenar e analisar dados, autonomia problema comandos toodevices com base em análises de dados ou agendas e expor informações e controle de recursos tooauthorized os usuários finais.

### <a name="information-devices-vs-special-purpose-devices"></a>Dispositivos de informações vs. dispositivos de finalidade especial
PCs, telefones e tablets são basicamente dispositivos de informações interativos. Os telefones e tablets são explicitamente otimizados em função de maximizar o tempo de vida da bateria. Eles preferencialmente desativar parcialmente quando não imediatamente interagir com uma pessoa, ou quando não fornecendo serviços como reproduzir música ou guiando proprietário tooa determinado local. De uma perspectiva de sistemas, esses dispositivos de tecnologia da informação atuam principalmente como proxies para as pessoas. Eles são "acionadores de pessoas" sugerindo ações e "sensores de pessoas" coletando informações. 

Dispositivos com finalidade especial, de linhas de produção de fábrica temperatura simples sensores toocomplex com milhares de componentes dentro deles, são diferentes. Esses dispositivos têm o escopo muito mais na finalidade e mesmo que eles fornecem alguma interface de usuário, elas são amplamente escopo toointerfacing com ou ser integradas em ativos em Olá, mundo físico. Eles medem e relatam circunstâncias ambientais, ativar válvulas, controlam servos, soam alarmes, alternar luzes e realizam várias outras tarefas. Eles ajudam a toodo de trabalho para que um dispositivo de informações é genérico muito, muito caro, muito grande ou muito frágil. finalidade concreta Olá impõe imediatamente seu design técnico como Olá bem disponível monetário orçamento sua produção e operação agendada do tempo de vida. combinação de saudação desses dois fatores-chave restringe Olá operacional alocação de energia, espaço físico e, portanto, o armazenamento disponível, computação disponíveis e recursos de segurança.  

Se algo "vai incorreto" com dispositivos controláveis automatizados ou remotos, por exemplo, defeitos físicos ou toowillful de defeitos de lógica de controle não autorizados invasões e manipulação. muitos de produção de Hello podem ter sido destruídos, edifícios podem ser sacados ou gravados para baixo e as pessoas podem ser chip ferido ou até mesmo. Isso é, obviamente, uma classe totalmente diferente de danos do que alguém maximizando o limite de um cartão de crédito roubado. Olá barreira de segurança para dispositivos que fazem coisas mover, e também para dados de sensor que eventualmente resulta em comandos que causam toomove coisas, deve ser maior que em qualquer cenário de transações bancárias ou comércio eletrônico. 

### <a name="device-control-and-device-data-interactions"></a>Controle de dispositivos e interações de dados do dispositivo
Dispositivos conectados de finalidade especial tem um número significativo de áreas da superfície potencial interação e padrões de interação, que deve ser considerado tooprovide uma estrutura para proteger o acesso digital toothose dispositivos. termo Hello "digital access" é usado toodistinguish aqui de todas as operações que são executadas por meio da interação direta do dispositivo onde a segurança de acesso é fornecida por meio do controle de acesso físico. Por exemplo, colocando dispositivo Olá em uma sala com um bloqueio na porta hello. Enquanto o acesso físico não pode ser negado usando hardware e software, medidas podem ser tomadas tooprevent o acesso físico dos principais toosystem interferência. 

Como podemos explorar os padrões de interação de hello, examinaremos "controle de dispositivo" e "dados de dispositivo" com o mesmo nível de atenção durante a modelagem de ameaças de hello. "Controle de dispositivo" pode ser classificado como qualquer informação fornecida tooa dispositivo por qualquer pessoa com objetivo de saudação de alteração ou influenciar o comportamento para seu estado ou saudação do seu ambiente. "Dados de dispositivo" podem ser classificados como todas as informações que um dispositivo emite tooany outro participante sobre seu estado e Olá observado o estado do seu ambiente. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Arquitetura de referência do hello Azure IoT de modelagem de ameaças
A Microsoft usa framework Olá descrito acima toodo ameaça de modelagem para IoT do Azure. Na seção de saudação abaixo, portanto, usamos exemplo concreto hello de arquitetura de referência do Azure IoT toodemonstrate como toothink sobre a modelagem de ameaça de IoT e como tooaddress Olá ameaças identificado. Em nosso caso, identificamos quatro áreas principais de foco:

* Dispositivos e fontes de dados,
* Transporte de dados,
* Dispositivo e processamento de eventos e
* Apresentação

![Modelagem de risco para a IoT do Azure](media/iot-security-architecture/iot-security-architecture-fig2.png) 

diagrama de saudação abaixo fornece uma exibição simplificada de arquitetura de IoT da Microsoft usando um modelo de diagrama de fluxo de dados que é usado pelo Olá, ferramenta de modelagem de ameaças do Microsoft:

![Modelagem de risco para a IoT do Azure usando a Ferramenta de Modelagem de Risco da Microsoft](media/iot-security-architecture/iot-security-architecture-fig3.png)

É importante toonote que Olá arquitetura separa os recursos de dispositivo e gateway hello. Isso permite Olá usuário tooleverage dispositivos de gateway que são mais seguros: são capazes de se comunicar com o gateway de nuvem de saudação usando protocolos seguros, que geralmente exige maior sobrecarga de processamento que um dispositivo nativo - como um termostato - pôde Fornece por conta própria. Na zona de serviços do Azure Olá, vamos supor que Olá que gateway de nuvem é representado por Olá serviço Azure IoT Hub.

### <a name="device-and-data-sourcesdata-transport"></a>Dispositivos e fontes de dados/transporte de dados
Esta seção explora a arquitetura de saudação descrita acima por meio de Lente de saudação da modelagem de ameaças e fornece uma visão geral de como vamos abordar alguns dos problemas inerentes hello. Vamos nos concentrar em Olá principais elementos de um modelo de ameaça:

* Processos (aqueles sob nosso controle e itens externos)
* Comunicação (também chamada de fluxos de dados)
* Armazenamento (também chamado de armazenamentos de dados)

#### <a name="processes"></a>Processos
Em cada uma das categorias de saudação descritas Olá arquitetura IoT do Azure, tentamos toomitigate existe um número de diferentes ameaças em informações da dados Olá diferentes estágios no: processo, a comunicação e o armazenamento. A seguir apresentamos uma visão geral de hello mais mais comuns para a categoria de "processo" Olá, seguido de uma visão geral de como eles podem ser melhor reduzidos: 

**Falsificação (S)**: um invasor pode extrair o material de chave de criptografia de um dispositivo, no nível de software ou hardware Olá e acessar sistema Olá posteriormente com um dispositivo físico ou virtual diferente em identidade Olá Olá Olá do dispositivo material de chave foi obtido. Uma boa ilustração são os controles remotos que podem ligar qualquer TV e são ferramentas populares dos pregadores de peças.

**D (Negação de Serviço)**: um dispositivo pode ficar incapaz de funcionar ou se comunicar interferindo com frequências de rádio ou cortando fios. Por exemplo, uma câmera de vigilância que teve sua conexão de rede ou de energia intencionalmente suprimida não relatará dados, de nenhuma maneira.

**Violação (T)**: um invasor pode parcialmente ou totalmente substituir Olá software em execução no dispositivo hello, permitindo potencialmente Olá Olá substituído software tooleverage original identidade do dispositivo Olá se hello material de chave ou Olá criptográfico recursos que contém o material de chave foram programa ilícito toohello disponíveis. Por exemplo, um invasor pode aproveitar toointercept material de chave extraída e suprimir os dados de dispositivo Olá no caminho de comunicação hello e substituí-lo com dados falsos que são autenticados com material de chave Olá roubado.

**Divulgação de informações (I)**: se o dispositivo hello está executando o software manipulado, esse software manipulado potencialmente pode vazar partes de toounauthorized de dados. Por exemplo, um invasor pode aproveitar extraído chave material tooinject em si no caminho de comunicação Olá entre o dispositivo hello e um gateway de campo ou de controlador ou gateway toosiphon as informações de nuvem.

**Elevação de privilégio (E)**: um dispositivo que executa a função específica pode ser forçado toodo algo mais. Por exemplo, uma válvula que é programado tooopen metade forma pode ser levado tooopen todos Olá maneira.

| **Componente** | **Ameaça** | **Mitigação** | **Risco** | **Implementação** |
| --- | --- | --- | --- | --- |
| Dispositivo |S |Atribuição de dispositivo de toohello de identidade e autenticação de dispositivo Olá |Substituindo o dispositivo ou parte de um dispositivo de saudação por algum outro dispositivo. Como sabemos que falamos dispositivo certo toohello? |Autenticação de dispositivo hello, usando a segurança de camada de transporte (TLS) ou IPSec. A infraestrutura deve dar suporte ao uso da PSK (chave pré-compartilhada) nos dispositivos que não conseguem lidar com a criptografia assimétrica completa. Aproveite o Azure AD, o [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Aplica o dispositivo de toohello mecanismos inviolável por exemplo, tornando difícil tooimpossible tooextract chaves e outro material criptográfico de dispositivo de saudação. |risco de saudação é se alguém é a violação dispositivo hello (interferência física). Como temos certeza de que o dispositivo não foi adulterado. |mitigação mais eficiente de saudação é um recurso de module (TPM) de plataforma confiável que permite armazenar chaves no circuito de no chip especial de quais Olá chaves não podem ser lido, mas só podem ser usadas para operações criptográficas que usam a chave hello, mas nunca divulguem chave Olá . Criptografia de memória do dispositivo de saudação. Gerenciamento de chaves para dispositivo hello. Assinatura de código de saudação. | |
| E |Com o controle de acesso do dispositivo hello. Esquema de autorização. |Se o dispositivo Olá permite para ações individuais toobe executadas com base em comandos de uma fonte externa, ou até mesmo comprometido sensores, ele permitirá ataque Olá tooperform operações caso contrário, não está acessível. |Com o esquema de autorização de dispositivo Olá | |
| Gateway de campo |S |Autenticando Olá campo gateway tooCloud Gateway (cert com base, PSK, declaração com base,...) |Se alguém pode falsificar o gateway de campo, pode se apresentar como qualquer dispositivo. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Todos os Olá mesmo armazenamento de chaves e preocupações de atestado de dispositivos em geral – caso melhor é usar o TPM. Extensão de 6LowPAN para IPSec toosupport sem fio Sensor de redes (WSN). |
| TRID |Proteger a saudação campo Gateway contra violação (TPM)? |Gateway que instruir o gateway de nuvem Olá pensar que está se comunicando toofield ataques de falsificação pode resultar em divulgação de informações e violação de dados |Criptografia da memória, TPM, autenticação. | |
| E |Mecanismo de controle de acesso para o gateway de campo | | | |

Aqui estão alguns exemplos de ameaças nesta categoria:

Falsificação: Um invasor pode extrair material de chave de criptografia de um dispositivo, no nível de software ou hardware hello e, subsequentemente, acesso de sistema Olá com um dispositivo físico ou virtual diferente na identidade de saudação do material de chave dispositivo Olá Olá foi obtido.

**Negação de Serviço**: um dispositivo pode ficar incapaz de funcionar ou de se comunicar interferindo em frequências de rádio ou cortando fios. Por exemplo, uma câmera de vigilância que teve sua conexão de rede ou de energia intencionalmente suprimida não relatará dados, de nenhuma maneira.

**Violação**: um invasor pode parcialmente ou totalmente substituir Olá software em execução no dispositivo hello, permitindo potencialmente Olá Olá substituído software tooleverage original identidade do dispositivo Olá se hello material de chave ou Olá criptográfico recursos que contém o material de chave foram programa ilícito toohello disponíveis.

**Violação**: uma câmera de vigilância que está mostrando uma imagem de espectro visível de um corredor vazio pode ser direcionada a uma fotografia de tal um corredor. Um sensor de fumaça ou incêndio pode relatar alguém segurando um isqueiro sob ele. Em ambos os casos, Olá dispositivo pode ser tecnicamente totalmente confiável para o sistema hello, mas ele reporta informações manipuladas.

**Violação**: um invasor pode aproveitar toointercept material de chave extraída e suprimir os dados de dispositivo Olá no caminho de comunicação hello e substituí-lo com dados falsos que são autenticados com material de chave Olá roubado.

**Violação**: um invasor pode parcialmente ou totalmente substituir Olá software em execução no dispositivo hello, permitindo potencialmente Olá Olá substituído software tooleverage original identidade do dispositivo Olá se hello material de chave ou Olá criptográfico recursos que contém o material de chave foram programa ilícito toohello disponíveis.

**Divulgação de informações**: se o dispositivo hello está executando o software manipulado, esse software manipulado potencialmente pode vazar partes de toounauthorized de dados.

**Divulgação de informações**: um invasor pode aproveitar extraído chave material tooinject em si no caminho de comunicação Olá entre o dispositivo hello e um gateway de campo ou de controlador ou gateway toosiphon as informações de nuvem.

**Negação de serviço**: dispositivo Olá pode ser desativado ou ativado em um modo em que a comunicação não é possível (que é intencional em muitas máquinas industriais).

**Violação**: dispositivo Olá pode ser reconfigurado toooperate em um estado desconhecido toohello sistema (fora de parâmetros de calibragem conhecido) de controle e, portanto, fornecer dados que podem ser interpretados incorretamente

**Elevação de privilégio**: um dispositivo que executa a função específica pode ser forçado toodo algo mais. Por exemplo, uma válvula que é programado tooopen metade forma pode ser levado tooopen todos Olá maneira.

**Negação de serviço**: Olá dispositivo pode ser ativado em um estado em que a comunicação não é possível.

**Violação**: dispositivo Olá pode ser reconfigurado toooperate em um estado desconhecido toohello sistema (fora de parâmetros de calibragem conhecido) de controle e, portanto, fornecer dados que podem ser interpretados incorretamente.

**Falsificação/violação/recusa**: se não protegidos (que é raramente Olá caso controles remotos do consumidor) um invasor pode manipular o estado de saudação de um dispositivo anonimamente. Uma boa ilustração são os controles remotos que podem ligar qualquer TV e são ferramentas populares dos pregadores de peças.

#### <a name="communication"></a>Comunicação
Ameaças em torno do caminho de comunicação entre dispositivos, dispositivos e gateways de campo e dispositivos e gateway de nuvem. tabela de saudação abaixo tem algumas diretrizes em torno de soquetes abertos no dispositivo/VPN hello:

| **Componente** | **Ameaça** | **Mitigação** | **Risco** | **Implementação** |
| --- | --- | --- | --- | --- |
| Hub IoT de dispositivo |TID |(D) Tráfego de saudação tooencrypt TLS (PSK/RSA) |Interceptação ou interferir comunicação Olá entre dispositivos hello e gateway Olá |Segurança em nível de protocolo de saudação. Com protocolos personalizados, precisamos toofigure como tooprotect-los. Na maioria dos casos, a saudação comunicação ocorre da saudação dispositivo toohello IoT Hub (dispositivo inicia a conexão de saudação). |
| Dispositivo |TID |(D) Tráfego de saudação tooencrypt TLS (PSK/RSA). |Leitura de dados em trânsito entre os dispositivos. Adulteração de dados de saudação. Sobrecarga de dispositivo de saudação com novas conexões |Segurança em nível de protocolo hello (MQTT/AMQP/HTTP/CoAP. Com protocolos personalizados, precisamos toofigure como tooprotect-los. atenuação Olá Olá ameaça DoS é toopeer dispositivos por meio de um gateway de nuvem ou campo e tê-los apenas atuar como clientes para a rede de saudação. Olá emparelhamento pode resultar em uma conexão direta entre pares de saudação após ter sido orientadas pelo gateway Olá |
| Dispositivo de entidade externa |TID |Emparelhamento de alta segurança de dispositivo de toohello Olá entidade externa |Dispositivo de toohello de conexão de interceptação hello. Comunicação de saudação interferindo com dispositivo Olá |Emparelhamento com segurança de dispositivo toohello da entidade externa Olá LE NFC/Bluetooth. Controlando o painel de Olá operacional do dispositivo da saudação (física) |
| Gateway de nuvem de Gateway de campo |TID |Tráfego de saudação tooencrypt TLS (PSK/RSA). |Interceptação ou interferir comunicação Olá entre dispositivos hello e gateway Olá |Segurança em nível de protocolo hello (MQTT/AMQP/HTTP/CoAP). Com protocolos personalizados, precisamos toofigure como tooprotect-los. |
| Gateway de nuvem do dispositivo |TID |Tráfego de saudação tooencrypt TLS (PSK/RSA). |Interceptação ou interferir comunicação Olá entre dispositivos hello e gateway Olá |Segurança em nível de protocolo hello (MQTT/AMQP/HTTP/CoAP). Com protocolos personalizados, precisamos toofigure como tooprotect-los. |

Aqui estão alguns exemplos de ameaças nesta categoria:

**Negação de serviço**: dispositivos restritos geralmente são sob ameaça DoS quando eles escutam ativamente para conexões de entrada ou datagramas não solicitadas em uma rede, pois um invasor pode abrir várias conexões em paralelo e não atender ou de serviço eles muito lentamente ou hello dispositivo pode ser inundado com tráfego não solicitado. Em ambos os casos, o dispositivo de saudação efetivamente pode ficar inoperante na rede de saudação.

**Falsificação, divulgação de informações**: dispositivos restritos e especial geralmente têm recursos de segurança de um-para-todos como proteção de PIN ou senha ou totalmente confiarão na rede Olá confiável, que significa que eles conceder acesso tooinformation quando um dispositivo estiver em Olá mesma rede e essa rede geralmente só é protegido por uma chave compartilhada. Que significa que quando Olá compartilhado toodevice secreta ou rede divulgada, é possível toocontrol Olá dispositivo ou observar dados emitidos de dispositivo de saudação.  

**Falsificação**: um invasor pode interceptar ou parcialmente substituir Olá difusão e FALSO Olá originador (man no meio de saudação)

**Violação**: um invasor pode interceptar ou parcialmente substituir difusão hello e enviar informações falsas 

**Divulgação de informações:** um invasor pode interceptar uma difusão e obter informações sem autorização **negação de serviço:** um invasor pode obstrução Olá broadcast sinal e negar a distribuição de informações

#### <a name="storage"></a>Armazenamento
Cada gateway do dispositivo e o campo tem alguma forma de armazenamento (temporário para dados de saudação do enfileiramento de mensagens, armazenamento de imagem do sistema operacional (SO)).

| **Componente** | **Ameaça** | **Mitigação** | **Risco** | **Implementação** |
| --- | --- | --- | --- | --- |
| Armazenamento de dispositivo |TRID |Criptografia de armazenamento, Olá logs de assinatura |Lendo dados de armazenamento de saudação (dados PII), adulteração de dados de telemetria. Violação de dados de controle de comando em cache ou enfileirados. Violação com pacotes de atualização de firmware ou de configuração enquanto armazenado em cache ou em fila localmente pode levar componentes tooOS e/ou sistema comprometidas |Criptografia, MAC (Message Authentication Code) ou assinatura digital. Onde for possível, controle de acesso forte por meio de permissões ou ACLs (listas de controle de acesso) de recurso. |
| Imagem do sistema operacional do dispositivo |TRID | |Violação com sistema operacional / substituir Olá OS componentes |Partição do sistema operacional somente leitura, imagem do sistema operacional assinada, criptografia |
| Armazenamento de Gateway de campo (dados de saudação de enfileiramento de mensagens) |TRID |Criptografia de armazenamento, Olá logs de assinatura |Lendo dados de armazenamento de saudação (dados PII), adulteração de dados de telemetria, adulteração enfileirada ou armazenado em cache dados de controle de comando. Violação com pacotes de atualização de firmware ou de configuração (destinados para dispositivos ou gateway de campo) enquanto armazenado em cache ou em fila localmente pode levar componentes tooOS e/ou sistema comprometidas |BitLocker |
| Imagem do sistema operacional do gateway de campo |TRID | |Violação com sistema operacional / substituir Olá OS componentes |Partição do sistema operacional somente leitura, imagem do sistema operacional assinada, criptografia |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Zona de gateway de nuvem/processamento de eventos e dispositivo
Um gateway de nuvem é um sistema que permite a comunicação remota do e gateways toodevices ou campo de diversos sites em espaço de rede pública, normalmente até um baseado em nuvem controle e dados de sistema de análise, uma federação de tais sistemas. Em alguns casos, um gateway de nuvem pode facilitar imediatamente acessem dispositivos de toospecial com a finalidade de terminais, como tablets e telefones. No contexto de saudação discutido aqui, "nuvem" destina-se toorefer tooa dedicado processamento de dados de sistema que não esteja associado toohello mesmo site como Olá anexado dispositivos ou gateways de campo e medidas operacionais impedir acesso físico de destino, mas não é necessariamente tooa infra-estrutura de "nuvem pública".  Um gateway de nuvem potencialmente pode ser mapeado para um gateway de rede virtualização sobreposição tooinsulate Olá nuvem e todos os seus dispositivos anexados ou gateways de campo de qualquer outro tráfego de rede. gateway de nuvem Olá em si não é um sistema de controle de dispositivo nem um processamento ou depósito de dados do dispositivo; Esses recursos de interajam com o gateway de nuvem hello. zona de gateway de nuvem de saudação inclui Olá nuvem próprio gateway junto com todos os gateways de campo e dispositivos direta ou indiretamente conectado tooit.

Gateway de nuvem é principalmente personalizados criados software em execução como um serviço com o gateway de campo toowhich pontos de extremidade expostos e dispositivos se conectem. Como tal, deve ser projetado tendo em mente a segurança. Siga o processo de [SDL](http://www.microsoft.com/sdl) para projetar e criar esse serviço. 

#### <a name="services-zone"></a>Zona de serviços
Um sistema de controle (ou controlador) é uma solução de software que interage com um dispositivo, ou um gateway de campo ou o gateway de nuvem para finalidade de saudação de controle de um ou vários dispositivos e/ou toocollect e/ou armazenamento de e/ou analisar os dados de dispositivo de apresentação, ou fins de controle subsequentes. Sistemas de controle são entidades de somente Olá no escopo de saudação desta discussão que podem facilitar a interação com as pessoas imediatamente. exceção Olá intermediário superfícies de controle físico em dispositivos, como uma opção que permite que uma pessoa tooturn dispositivo de saudação desativar ou alterar outras propriedades, e para o qual não há nenhum equivalente funcional que pode ser acessado digitalmente. 

Superfícies de controle físicos intermediários são aquelas em que qualquer tipo de lógica de controle restringe função hello da superfície de controle físico hello, de modo que uma função equivalente pode ser iniciada remotamente ou entrada está em conflito com entrada remota pode ser evitados – tais intermediadas superfícies de controle são conceitualmente anexado tooa controle local system que aproveita Olá mesma funcionalidade subjacente que qualquer outro sistema de controle remoto que Olá dispositivo pode ser anexado tooin paralela. Computação podem ser lidas em nuvem toohello principais ameaças [Alliance de segurança de nuvem (CSA)](https://cloudsecurityalliance.org/research/top-threats/) página.

## <a name="additional-resources"></a>Recursos adicionais
Consulte toohello artigos para obter informações adicionais a seguir:

* [Ferramenta de modelagem de ameaças do SDL](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Arquitetura de referência da IoT do Microsoft Azure](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

