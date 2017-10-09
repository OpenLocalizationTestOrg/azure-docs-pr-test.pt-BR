---
title: "Considerações de aaaSecurity para Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Aborda considerações de segurança para usar o Proxy de Aplicativo do Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Considerações de segurança para acessar aplicativos remotamente com o Proxy de Aplicativo do Azure AD

Este artigo explica como o Proxy de Aplicativo do Azure Active Directory fornece um serviço seguro para publicar e acessar aplicativos remotamente.

Olá seguinte diagrama mostra como o Azure AD permite que aplicativos de locais de tooyour de acesso remoto seguro.

 ![Diagrama de acesso remoto por meio do Proxy de Aplicativo do Azure AD](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>Benefícios de segurança

Proxy de aplicativo do Azure AD oferece Olá benefícios de segurança a seguir:

### <a name="authenticated-access"></a>Acesso autenticado 

Se você escolher toouse Active Directory do Azure pré-autenticação, somente conexões autenticadas podem acessar sua rede.

Proxy de aplicativo do Azure AD depende de saudação do AD do Azure serviço de token segurança (STS) para todas as autenticações.  Pré-autenticação, por natureza, bloqueia um número significativo de ataques anônimos, porque somente identidades autenticadas podem acessar o aplicativo de back-end de saudação.

Se você escolher Passagem como seu método de pré-autenticação, não terá esse benefício. 

### <a name="conditional-access"></a>Acesso condicional

Aplica controles de política mais ricas antes de conexões de rede tooyour são estabelecidas.

Com [acesso condicional](active-directory-conditional-access-azuread-connected-apps.md), você pode definir restrições em que o tráfego é permitido tooaccess seus aplicativos de back-end. É possível criar políticas que restrinjam entradas com base no local, na força da autenticação e no perfil de risco do usuário.

Você também pode usar políticas de autenticação multifator de tooconfigure de acesso condicional, adicionando outra camada de autenticações de usuário de tooyour de segurança. 

### <a name="traffic-termination"></a>Encerramento de tráfego

Todo o tráfego é terminado em nuvem hello.

Como o Proxy de aplicativo do Azure AD é um proxy reverso, todos os aplicativos de tooback a fim de tráfego é finalizada com serviço de saudação. Olá sessão pode obter restabelecida com o servidor de back-end hello, que significa que os servidores de back-end não são expostos tráfego toodirect HTTP. Essa configuração significa que você terá uma proteção melhor contra ataques direcionados.

### <a name="all-access-is-outbound"></a>Todo o acesso é de saída 

Rede corporativa do toohello tooopen conexões de entrada não é necessário.

Conectores de Proxy de aplicativo só usam toohello AD do Azure serviço de Proxy de aplicativo conexões de saída, o que significa que não é necessário tooopen portas de firewall para conexões de entrada. Proxies tradicionais necessária uma rede de perímetro (também conhecido como *DMZ*, *zona desmilitarizada*, ou *sub-rede filtrada*) e a permissão de acesso toounauthenticated conexões na borda da rede de saudação. Neste cenário necessárias muitos investimentos adicionais em aplicativo web tráfego de tooanalyze produtos de firewall e oferecem adição proteções toohello ambiente. Com o Proxy de Aplicativo, você não precisa de uma rede de perímetro porque todas as conexões são de saída e ocorrem por um canal seguro.

Para saber mais sobre conectores, veja [Noções básicas sobre conectores de proxy de aplicativo do Azure AD](application-proxy-understand-connectors.md).

### <a name="cloud-scale-analytics-and-machine-learning"></a>Machine learning e análise em escala de nuvem 

Obtenha proteção de segurança de ponta.

Porque ele é parte do Active Directory do Azure, o Proxy de aplicativo pode aproveitar [Azure AD Identity Protection](active-directory-identityprotection.md)com inteligência com base em aprendizado de máquina e dados de saudação Microsoft Security Response Center e Digital Crimes Unit. Juntos, identificamos proativamente contas comprometidas e oferecemos proteção em tempo real em conexões de alto risco. Levamos em consideração vários fatores, como acesso de dispositivos infectados por meio de redes que mantêm o anonimato, bem como de locais atípicos e improváveis.

Muitos desses relatórios e eventos já estão disponíveis por meio de uma API para integração com as informações de segurança e sistemas de gerenciamento (SIEM) do evento.

### <a name="remote-access-as-a-service"></a>Acesso remoto como serviço

Você não tem tooworry sobre manutenção e aplicação de patch servidores locais.

A não aplicação de patches no software ainda é responsável por um grande número de ataques. Proxy de aplicativo do Azure AD é um serviço de escala da Internet que possui a Microsoft, assim você sempre obter atualizações e patches de segurança mais recentes do hello.

segurança de saudação tooimprove de aplicativos publicados pelo Proxy de aplicativo do Azure AD, podemos bloquear robôs do rastreador da web de indexação e o arquivamento de seus aplicativos. Cada vez que um robô rastreador da Web tentar recuperar as configurações de robôs para um aplicativo publicado, o Proxy de Aplicativo responderá com um arquivo robots.txt que inclui `User-agent: * Disallow: /`.

## <a name="under-hello-hood"></a>Bastidores Olá

O Proxy de Aplicativo do Azure AD consiste em duas partes:

* Olá serviço baseado em nuvem: este serviço é executado no Azure e é onde as conexões de cliente/usuário externo de saudação são feitas.
* [Olá conector local](application-proxy-understand-connectors.md): um componente de local, conector Olá escuta solicitações de serviço de Proxy de aplicativo de saudação do AD do Azure e gerencia aplicativos internos de toohello de conexões. 

Um fluxo entre conector hello e serviço de Proxy de aplicativo hello é estabelecido quando:

* conector de saudação é configurada pela primeira vez.
* conector de saudação extrai informações de configuração de saudação serviço Proxy de aplicativo.
* Um usuário acessa um aplicativo publicado.

>[!NOTE]
>Todas as comunicações ocorrem por SSL, e eles sempre são originadas Olá conector toohello serviço Proxy de aplicativo. serviço de saudação é de saída apenas.

conector de saudação usa um toohello de tooauthenticate de certificado de cliente serviço de Proxy de aplicativo para quase todas as chamadas. Olá somente exceção toothis processo é etapa de configuração inicial do hello, em que o certificado de cliente Olá é estabelecido.

### <a name="installing-hello-connector"></a>Instalar o conector do hello

Quando o conector de saudação é configurado pela primeira vez, Olá eventos de fluxo a seguir ocorrem:

1. serviço de toohello de registro do conector Olá ocorre como parte da instalação de saudação do conector de saudação. Os usuários é solicitado tooenter suas credenciais de administrador do AD do Azure. O token obtido dessa autenticação é apresentado toohello serviço de Proxy de aplicativo do Azure AD.
2. Olá serviço Proxy de aplicativo avalia token hello. Isso garante que um administrador da empresa no locatário Olá Olá token foi emitido para o usuário hello está. Se o usuário de saudação não for um administrador, o processo de saudação é encerrado.
3. conector Hello gera uma solicitação de certificado de cliente e passá-lo, juntamente com toohello de token, Olá serviço Proxy de aplicativo. por sua vez, serviço Olá verifica o token hello e faz a solicitação de certificado de cliente de saudação.
4. conector de Olá usa o certificado de cliente Olá para comunicação futura com hello serviço Proxy de aplicativo.
5. conector de saudação realiza uma recepção inicial dos dados de configuração do sistema de saudação do serviço hello usando seu certificado de cliente, e agora está pronto tootake solicitações.

### <a name="updating-hello-configuration-settings"></a>Atualizando as definições de configuração de saudação

Sempre que Olá serviço Proxy de aplicativo de atualizações de definições de configuração de saudação, Olá eventos de fluxo a seguir ocorrem:

1. conector Olá conecta toohello configuração os pontos de extremidade Olá serviço Proxy de aplicativo usando seu certificado de cliente.
2. Depois que o certificado de cliente Olá foi validado, Olá serviço Proxy de aplicativo retorna toohello conector de dados da configuração (por exemplo, grupo de conector Olá Olá conector deve ser parte do).
3. Se o certificado atual Olá é mais de 180 dias, o conector hello gera uma nova solicitação de certificado, que efetivamente atualiza o certificado de cliente de saudação a cada 180 dias.

### <a name="accessing-published-applications"></a>Acesso a aplicativos publicados

Quando os usuários acessam um aplicativo publicado, hello seguintes eventos ocorrem entre o serviço de Proxy de aplicativo hello e o conector de Proxy de aplicativo hello:

1. [serviço de saudação autentica o usuário Olá para o aplicativo hello](#the-service-checks-the-configuration-settings-for-the-app)
2. [serviço de saudação faz uma solicitação na fila de conector Olá](#The-service-places-a-request-in-the-connector-queue)
3. [Um conector processa a solicitação de saudação da fila de saudação](#the-connector-receives-the-request-from-the-queue)
4. [conector de saudação aguarda uma resposta](#the-connector-waits-for-a-response)
5. [usuário de toohello de dados do Hello serviço fluxos](#the-service-streams-data-to-the-user)

toolearn mais sobre o que acontece em cada uma dessas etapas, continue lendo.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. serviço de Olá autentica o usuário de saudação para o aplicativo hello

Se você configurou Olá aplicativo toouse passagem como seu método de pré-autenticação, etapas Olá nesta seção serão ignoradas.

Se você configurou Olá toopreauthenticate de aplicativo com o AD do Azure, os usuários são redirecionado toohello tooauthenticate de STS do AD do Azure e hello etapas a seguir ocorrem:

1. Proxy de aplicativo procura qualquer requisitos de política de acesso condicional para aplicativos específicos hello. Essa etapa garante que Olá foi atribuída ao usuário toohello aplicativo. Se a verificação em duas etapas é necessária, sequência de autenticação Olá solicita Olá usuário um segundo método de autenticação.

2. Depois que todas as verificações foram aprovadas, Olá STS do AD do Azure emite um token assinado para o aplicativo hello e redireciona Olá usuário back toohello serviço Proxy de aplicativo.

3. Proxy de aplicativo verifica que esse token Olá foi emitido aplicativo hello de toocorrect. Ele executa outras verificações também, como garantir que Olá token foi assinado pelo AD do Azure e que ele ainda estiver dentro de janela válido hello.

4. Proxy de aplicativo define uma tooindicate de cookie de autenticação criptografada que o aplicativo de toohello autenticação ocorreu. Olá cookie inclui um carimbo de hora de expiração é baseado em token de saudação do AD do Azure e outros dados, como nome de usuário Olá Olá autenticação se baseia. Olá cookie é criptografado com uma chave privada conhecida toohello serviço Proxy de aplicativo.

5. Aplicativo Proxy redirecionamentos Olá usuário toohello back solicitou o URL.

Se qualquer parte das etapas de pré-autenticação Olá falhar, solicitação de saudação do usuário foi negada e usuário Olá é mostrado uma mensagem indicando a origem de saudação de problema de saudação.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. serviço Olá faz uma solicitação na fila de conector Olá

Os conectores mantêm toohello de abrir uma conexão de saída serviço Proxy de aplicativo. Quando uma solicitação chega, serviço Olá enfileira solicitação Olá em uma das conexões de abrir Olá para Olá conector toopick backup.

solicitação Olá inclui itens de aplicativo hello, como cabeçalhos de solicitação hello, dados do cookie Olá criptografado, Olá usuário fazer Olá solicitação e Olá ID da solicitação Embora os dados do cookie criptografado Olá são enviados com solicitação hello, cookie de autenticação de saudação em si não é.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. conector Olá processa a solicitação de saudação da fila de saudação. 

Proxy de aplicativo com base na solicitação de Olá, executa uma das seguintes ações de saudação:

* Se a solicitação de saudação é uma operação simples (por exemplo, não há nenhum dado dentro do corpo de hello, sem um RESTful *obter* solicitação), conector de saudação faz um recurso interno do destino de toohello de conexão e, em seguida, aguarda uma resposta.

* Se a solicitação de saudação tiver dados associados a ele no corpo da saudação (por exemplo, um RESTful *POST* operação), conector Olá faz uma conexão de saída por meio de instância de Proxy de aplicativo hello cliente certificado toohello. Ele faz com que dados conexão toorequest hello e abrir um recurso interno de toohello de conexão. Depois de receber a solicitação de saudação do conector de saudação, o serviço de Proxy de aplicativo hello começa a aceitar o conteúdo de usuário hello e encaminha toohello o conector de dados. conector de Hello, por sua vez, encaminha os recursos internos do hello dados toohello.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. conector de Olá aguarda uma resposta.

Depois de fazer a solicitação hello e transmissão de toohello todo o conteúdo final é concluído, conector Olá aguarda uma resposta.

Depois de receber uma resposta, conector Olá faz com que um serviço de Proxy de aplicativo de toohello de conexão de saída, tooreturn Olá detalhes do cabeçalho e iniciar o fluxo de dados de retorno de saudação.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. Olá serviço fluxos dados toohello o usuário. 

Algum processamento do aplicativo hello pode ocorrer aqui. Se você configurou URLs ou cabeçalhos de tootranslate do Proxy de aplicativo em seu aplicativo, o que o processamento ocorre conforme necessário durante esta etapa.


## <a name="next-steps"></a>Próximas etapas

[Considerações de topologia de rede ao usar o Proxy de Aplicativo do Azure AD](application-proxy-network-topology-considerations.md)

[Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)
