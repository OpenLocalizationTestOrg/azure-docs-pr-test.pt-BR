O gerenciamento de identidades é tão importante na nuvem pública Olá pois ela está no local. toohelp com isso, o Azure suporta várias tecnologias de identidade de nuvem diferente. Entre elas:

* Você pode executar o Windows Server Active Directory (geralmente chamado apenas AD) na nuvem de saudação usando máquinas virtuais criadas com máquinas virtuais do Azure. Essa abordagem faz sentido quando você estiver usando o Azure tooextend seu datacenter local para nuvem hello.
* Você pode usar o Active Directory do Azure toogive seus usuários único logon muito[Software como serviço (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) aplicativos. Por exemplo, o Office 365 da Microsoft utiliza essa tecnologia, e aplicativos executados no Azure ou outras plataformas na nuvem também podem usá-lo.
* Aplicativos em execução no hello nuvem ou local pode usar o Active Directory Access Control do Azure toolet usuários fazer logon usando identidades do Facebook, Google, Microsoft e outros provedores de identidade.

Este artigo descreve todas essas três opções.

## <a name="table-of-contents"></a>Sumário
* [Executando o Active Directory do Windows Server em máquinas virtuais](#adinvm)
* [Usando o Active Directory do Azure](#ad)
* [Usando o Controle de Acesso do Active Directory do Azure](#ac)

## <a name="adinvm"></a>Executando o Active Directory do Windows Server em máquinas virtuais
Executar o AD do Windows Server em máquinas virtuais do Azure é muito semelhante a executá-lo localmente. [Figura 1](#fig1) mostra um exemplo típico de como isso acontece.

![Active Directory do Azure na Máquina Virtual](./media/identity/identity_01_ADinVM.png)

<a name="Fig1"></a>Figura 1: O Active Directory do Windows Server pode executar no datacenter do Azure máquinas virtuais conectadas tooan organização local usando a rede Virtual do Azure.

O exemplo hello mostrado aqui, AD do Windows Server está em execução em máquinas virtuais criadas usando máquinas virtuais do Azure, a tecnologia da plataforma Olá IaaS. Essas VMs e alguns outros são agrupados em um rede virtual conectado tooan no data center local usando a rede Virtual do Azure. rede virtual Olá Entalha-out de um grupo de máquinas virtuais de nuvem que interagem com a rede de local de saudação por meio de uma conexão de rede virtual privada (VPN). Fazer isso permite que essas máquinas virtuais do Azure se parecer com qualquer outra sub-rede toohello local datacenter. Como mostra a Figura hello, duas dessas VMs estão sendo executados controladores de domínio do AD do Windows Server. Olá outras máquinas virtuais na rede virtual Olá pode estar executando aplicativos, como o SharePoint, ou que está sendo usado de alguma outra maneira, como para desenvolvimento e teste. Olá local datacenter também está executando dois controladores de domínio do AD do Windows Server.

Há várias opções de conexão Olá para controladores de domínio na nuvem Olá com aqueles em execução no local:

* Tornar todas elas parte de um único domínio do Active Directory.
* Criar separado AD domínios locais e na nuvem Olá que fazem parte da saudação mesma floresta.
* Criar separadas florestas do AD no local e a nuvem de saudação e conecte a florestas hello usando relações de confiança entre florestas ou Windows Server Active Directory Federation Services (AD FS), que também pode ser executado em máquinas virtuais no Azure.

Qualquer opção feita, um administrador deve garantir que solicitações de autenticação de usuários locais vão toocloud controladores de domínio somente quando necessário, como nuvem de toohello link Olá é provavelmente toobe mais lento do que as redes locais. Tooconsider de outro fator na conexão de nuvem e os controladores de domínio local é o tráfego de saudação gerado pela replicação. Controladores de domínio na nuvem Olá são normalmente em seu próprio site AD, que permite que um tooschedule administrador frequência a replicação é feita. O Azure cobra pelo tráfego enviado fora de um datacenter do Azure, embora não de bytes enviados em que podem afetar as opções de replicação do administrador hello. Também vale a pena salientar que, enquanto o Azure fornece seu próprio suporte do Sistema de Nomes de Domínios (DNS), nesse serviço faltam recursos exigidos pelo Active Directory (como suporte para registros de DNS dinâmico e SRV). Por isso, executando o Windows Server AD no Azure requer configurar seus próprios servidores DNS na nuvem hello.

Executar o AD do Windows Server em VMs do Azure pode fazer sentido em várias situações diferentes. Estes são alguns exemplos:

* Se você estiver usando máquinas virtuais do Azure como uma extensão de seu próprio data center, você pode executar aplicativos na nuvem Olá que precisam de coisas de toohandle de controladores de domínio local, como solicitações de autenticação integrada do Windows ou as consultas LDAP. SharePoint, por exemplo, interage com frequência com o Active Directory, e então Embora seja possível toorun um farm do SharePoint no Azure usando um diretório local, configurando controladores de domínio na nuvem Olá significativamente melhorará o desempenho. (É importante toorealize que isso não é necessariamente obrigatório, no entanto, vários aplicativos podem executar com êxito na nuvem de saudação usando somente os controladores de domínio local.)
* Suponha que uma filial longínqua não tem Olá recursos toorun seus próprios controladores de domínio. Atualmente, seus usuários devem autenticar controladores toodomain Olá outro lado da Olá, mundo - logons estão lentos. Executando o Active Directory no Azure em um datacenter da Microsoft mais próximo pode acelerar isso sem a necessidade de mais servidores na filial hello.
* Uma organização que usa o Azure para recuperação de desastres pode manter um pequeno conjunto de máquinas virtuais ativas na nuvem hello, incluindo um controlador de domínio. Em seguida, pode ser preparada tooexpand este site como tootake necessário sobre falhas em outro lugar.

Existem também outras possibilidades. Por exemplo, você não é necessário tooconnect Windows Server AD em Olá nuvem tooan datacenter local. Se você quisesse toorun um farm do SharePoint que serviu a um conjunto específico de usuários, por exemplo, todos os quais seriam login exclusivamente com identidades baseadas em nuvem, você pode criar uma floresta autônomo no Azure. A maneira como você usa essa tecnologia depende de quais são suas metas. (Para obter orientações mais detalhadas sobre como usar o AD do Windows Server com o Azure, [clique aqui](http://msdn.microsoft.com/library/windowsazure/jj156090.aspx).)

## <a name="ad"></a>Usando o Active Directory do Azure
Conforme os aplicativos SaaS tornam-se cada vez mais comuns, eles geram uma questão óbvia: que tipo de serviço de diretório esses aplicativos baseados em nuvem devem usar? Pergunta de toothat de resposta da Microsoft é o Azure Active Directory.

Há duas opções principais para usar este serviço de diretório na nuvem hello:

* Indivíduos e organizações que usam somente aplicativos SaaS podem depender do Active Directory do Azure como seu único serviço de diretório.
* As organizações que executam o Windows Server Active Directory podem conectar seu tooAzure de diretório local do Active Directory e depois usá-lo toogive aos usuários um único logon tooSaaS aplicativos.

[Figura 2](#fig2) ilustra Olá primeira dessas duas opções, em que o Active Directory do Azure é tudo o que é necessário.

![Active Directory do Azure na Máquina Virtual](./media/identity/identity_02_AD.png)

<a name="fig2"></a>Figura 2: Active Directory do Azure oferece a usuários de uma organização aplicativos tooSaaS de logon único, incluindo o Office 365.

Como mostra a Figura hello, o AD do Azure é um serviço de multilocatário. Isso significa que ele pode suportar simultaneamente várias organizações, armazenando informações de diretório sobre os usuários em cada um deles. Neste exemplo, um usuário da organização A está tentando tooaccess um aplicativo SaaS. Este aplicativo pode ser parte do Office 365, como SharePoint Online, ou pode ser outra coisa — aplicativos não Microsoft também podem usar essa tecnologia. Como o AD do Azure oferece suporte a protocolo de saudação SAML 2.0, tudo o que é necessário de um aplicativo é Olá capacidade toointeract usando esse padrão do setor. (De fato, os aplicativos que usam o AD do Azure podem ser executados em qualquer datacenter, não apenas em um datacenter do Azure.)

processo de saudação começa quando o usuário Olá acessa um aplicativo SaaS (etapa 1). toouse este aplicativo, o usuário Olá deve apresentar um token emitido pelo AD do Azure.

Esse token contém informações que identificam o usuário hello e foi assinado digitalmente pelo AD do Azure. token de saudação tooget, Olá usuário autentica si tooAzure AD fornecendo um nome de usuário e senha (etapa 2). AD do Azure, em seguida, retorna o token Olá ele precisa (etapa 3).

Esse token é enviado toohello SaaS aplicativo (etapa 4), que valida a assinatura do token hello e usa seu conteúdo (etapa 5). Normalmente, o aplicativo hello usará informações de identidade Olá token Olá contém toodecide que o usuário de saudação de informações é permitido tooaccess e talvez de outras maneiras.

Se o aplicativo hello precisa de mais informações sobre o usuário Olá que contidas no token hello, ele pode solicitá-la diretamente do AD do Azure usando a API do Azure AD Graph hello (etapa 6). Na versão inicial de saudação do AD do Azure, o esquema de diretório Olá é muito simple: ele contém apenas os usuários e grupos e relações entre eles. Os aplicativos podem usar esse toolearn informações sobre conexões entre os usuários. Por exemplo, suponha que um aplicativo precisa tooknow que gerente deste usuário é toodecide se ele é parte de toosome de acesso de dados. Ele pode ser aprender consultando o Azure AD por meio de saudação API do Graph.

Olá Graph API usa um protocolo RESTful comum, o que torna simples toouse da maioria dos clientes, incluindo dispositivos móveis. Olá API também oferece suporte a extensões de saudação definidas por OData, adicionando itens, como um linguagem de consulta toolet clientes acessar dados de maneiras mais úteis. (Para saber mais sobre OData, consulte [Apresentação do OData](http://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf).) Como Olá Graph API pode ser usado toolearn sobre as relações entre os usuários, ele permite que aplicativos entender o gráfico de social Olá incorporada no esquema de saudação do AD do Azure para uma determinada organização (que é por isso que é chamado hello API do Graph). E tooauthenticate próprio solicitações tooAzure AD para a Graph API, um aplicativo usa OAuth 2.0.

Se uma organização não usa o Active Directory do Windows Server, ele não tem servidores locais ou domínios - e se baseia apenas em aplicativos de nuvem que usam o AD do Azure, usar apenas esse diretório na nuvem daria usuários único logon tooall da empresa Olá deles. Apesar de esse cenário se tornar mais comum todos os dias, a maioria das organizações ainda usa domínios locais criados com o Active Directory do Windows Server. O AD do Azure tem uma função útil tooplay aqui, assim como [Figura 3](#fig3) mostra.

![Active Directory do Azure na máquina Virtual](./media/identity/identity_03_AD.png)
<a id="fig3"></a>Figura 3: uma organização pode federar Active Directory do Windows Server com o Active Directory do Azure toogive seus aplicativos de tooSaaS de logon único de usuários.

Nesse cenário, um usuário na organização B deseja tooaccess um aplicativo SaaS. Antes de fazer isso, os administradores do diretório da organização Olá devem estabelecer uma relação de federação com o Azure AD usando o AD FS, como mostra a Figura hello. Esses administradores também devem configurar a sincronização de dados entre local Windows Server Olá organização AD e do AD do Azure. Isso copia automaticamente informações de usuário e grupo de saudação local diretório tooAzure AD. Observe que isso permite: em vigor, organização hello está estendendo seu diretório local para a nuvem de saudação. A combinação de Windows Server AD e o Azure AD dessa maneira traz organização Olá um serviço de diretório que pode ser gerenciado como uma única entidade, ao mesmo tempo, um volume no local e na nuvem de saudação.

toouse AD do Azure, Olá usuário primeiro faz logon no domínio de Active Directory local tooher como de costume (etapa 1). Quando ela tenta aplicativo SaaS da saudação tooaccess (etapa 2), o processo de federação de saudação resulta no Azure AD emitir um token para este aplicativo (etapa 3) ela. (Para saber mais sobre o funcionamento da federação, consulte [Identidade baseada em declarações para Windows: tecnologias e cenários](http://www.davidchappell.com/writing/white_papers/Claims-Based_Identity_for_Windows_v3.0--Chappell.docx).) Como antes, esse token contém informações que identificam o usuário hello e foi assinado digitalmente pelo AD do Azure. Esse token é enviado toohello SaaS aplicativo (etapa 4), que valida a assinatura do token hello e usa seu conteúdo (etapa 5). E está no cenário anterior hello, Olá SaaS pode usar o aplicativo hello Graph API toolearn mais sobre este usuário se necessário (etapa 6).

Hoje em dia, o AD do Azure AD não é uma substituição completa do AD do Windows Server local. Como mencionado anteriormente, o diretório de nuvem de saudação tem um esquema muito mais simples e coisas como a política de grupo, informações de toostore Olá capacidade sobre máquinas e suporte para LDAP também está ausente. (Na verdade, um computador Windows não pode ser configurado toolet os usuários fazem logon em tooit usando apenas o AD do Azure, isso não é um cenário com suporte.) Em vez disso, metas de saudação inicial do AD do Azure incluem permitindo que aplicativos de acesso de usuários corporativos na nuvem Olá sem manter um logon separado e liberando local Administradores de diretório do seu diretório local com a sincronização manualmente cada aplicativo SaaS que sua organização usa. Ao longo do tempo, no entanto, espera que esse tooaddress de serviço de diretório uma grande variedade de cenários de nuvem.

## <a name="ac"></a>Usando o Controle de Acesso do Active Directory do Azure
Tecnologias de identidade baseados em nuvem podem ser usado toosolve uma variedade de problemas. Active Directory do Azure pode dar a usuários de uma organização aplicativos SaaS de toomultiple de logon único, por exemplo. Mas, tecnologias de identidade na nuvem Olá também podem ser usadas de outras maneiras.

Por exemplo, suponha que um aplicativo deseja toolet seus usuários de log usando os tokens emitidos por vários *provedores de identidade (IdPs)*. Existem diversos provedores de identidade diferentes atualmente, incluindo Facebook, Google, Microsoft e outros, e frequentemente os aplicativos permitem que os usuários entrem usando uma dessas identidades. Por que deve um aplicativo se preocupar toomaintain sua própria lista de usuários e senhas quando ele em vez disso, pode contar com identidades que já existem? Aceitar identidades existentes simplifica a vida útil para os usuários que têm um menos tooremember de nome de usuário e senha, e pessoas Olá criar suas próprias listas de nomes de usuário e senhas de aplicativo hello, que não precisem mais toomaintain.

Mas enquanto cada provedor de identidade emite algum tipo de token, esses tokens não padrão — cada IdP tem seu próprio formato. Além disso, as informações de saudação nestes tokens também não padrão. Um aplicativo que deseja tooaccept tokens emitidos por, digamos, Facebook, Google e Microsoft é enfrentam Olá de escrever código exclusivo toohandle cada um desses formatos diferentes.

Mas por que fazer isso? Em vez disso, por que não criar um intermediário que possa gerar um único formato de token com uma representação comum de informações de identidade? Essa abordagem seria tornar a vida mais simples para desenvolvedores de saudação que criam aplicativos, já que agora precisam toohandle somente um tipo de token. Azure controle de acesso do Active Directory faz exatamente isso, a fornecendo um intermediário na nuvem Olá para trabalhar com vários tokens. [Figura 4](#fig4) mostra como is funciona

![Active Directory do Azure na máquina Virtual](./media/identity/identity_04_IdentityProviders.png)
<a id="fig4"></a>Figura 4: controle de acesso do Azure Active Directory torna mais fácil para aplicativos tooaccept identidade tokens emitidos por diferentes provedores de identidade.

processo de saudação começa quando um usuário tenta aplicativo hello de tooaccess em um navegador. aplicativo Hello redireciona o tooan IdP de sua escolha (e esse aplicativo hello também confia). Ele autentica por conta própria toothis IdP, como digitando um nome de usuário e senha (etapa 1) e Olá IdP retorna um token que contém informações sobre sua (etapa 2).

Como mostra a Figura hello, controle de acesso oferece suporte a uma variedade de diferentes IdPs baseado em nuvem, incluindo contas criadas pelo Google, Yahoo, Facebook, Microsoft (anteriormente conhecido como Windows Live ID) e qualquer provedor OpenID. Ele também dá suporte a identidades criadas usando o Azure Active Directory e, por meio de federação com o AD FS, o Active Directory do Windows Server. meta de Olá é toocover identidades de hello mais comumente usada hoje, eles são emitidos pelas IdPs no local ou nuvem de saudação.

Depois que o navegador do usuário Olá tem um token de IdP do seu IdP escolhido, ele envia esse token tooAccess controle (etapa 3). Controle de acesso valida o token hello, certificando-se de que realmente foi emitido por esse IdP, em seguida, cria um novo token de acordo com as regras de toohello que foram definidas para este aplicativo. Como o Active Directory do Azure, controle de acesso é um serviço multilocatário, mas locatários Olá são aplicativos em vez de organizações de cliente. Cada aplicativo pode obter seu próprio namespace, como mostra a Figura Olá e pode definir várias regras sobre autorização e muito mais.

Essas regras permitem que o administrador de cada aplicativo defina como os tokens de vários IdPs devem ser transformados em um token do Controle de Acesso. Por exemplo, se IdPs diferentes usam tipos diferentes para representar os nomes de usuário, as regras do Controle de Acesso podem transformar todos eles em um tipo de nome de usuário comum. Controle de acesso, em seguida, envia esse novo navegador token toohello back (etapa 4), que envia toohello aplicativo (etapa 5). Depois que ele tem um token de controle de acesso Olá, o aplicativo hello verifica esse token realmente foi emitido pelo controle de acesso e usa as informações de saudação contém (etapa 6).

Durante esse processo pode parecer um pouco complicado, na verdade faz vida significativamente mais simples para o criador de saudação do aplicativo hello. Em vez de lidar com vários tokens que contém informações diferentes, o aplicativo hello pode aceitar identidades emitidas por vários provedores de identidade ao ainda receber apenas um único token com informações conhecidas. Além disso, em vez de precisar que toobe cada aplicativo configurado tootrust IdPs vários, em vez disso, essas relações de confiança são mantidas pelo controle de acesso: um aplicativo só precisa confiar.

Vale a pena observar que nada sobre o controle de acesso está associado tooWindows – ela também pode ser usada por um aplicativo de Linux que aceita somente identidades Google e Facebook. E, mesmo que o controle de acesso é parte da saudação família do Active Directory do Azure, você pode pensar nele como um serviço totalmente distinto do que foi descrito na seção anterior hello. Embora as duas tecnologias funcionam com a identidade, eles abordam problemas completamente diferentes (embora a Microsoft disse que espera toointegrate Olá dois em algum momento).

Trabalhar com identidade é importante em praticamente todos os aplicativos. meta de saudação do controle de acesso é toomake mais fácil para aplicativos de toocreate de desenvolvedores que aceitam identidades de provedores de identidade diferentes. Ao colocar este serviço na nuvem hello, Microsoft tornou disponível tooany aplicativo em execução em qualquer plataforma.

## <a name="about-hello-author"></a>Sobre Olá autor
David Chappell é diretor da Chappell & Associates [www.davidchappell.com](http://www.davidchappell.com) em São Francisco, Califórnia.

