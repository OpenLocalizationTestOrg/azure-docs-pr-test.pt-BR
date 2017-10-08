---
title: aaaHow toouse o controle de acesso (Java) | Microsoft Docs
description: Saiba como toodevelop e o uso de controle de acesso com Java no Azure.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>Como tooAuthenticate usuários da Web com o Azure acesso de controle de serviço usando o Eclipse
Este guia mostrará como toouse hello Azure Access Control Service (ACS) dentro de saudação Kit de ferramentas do Azure para Eclipse. Para obter mais informações sobre o ACS, consulte Olá [próximas etapas](#next_steps) seção.

> [!NOTE]
> Olá filtro de controle de serviços de acesso do Azure é uma visualização de tecnologia da comunidade. Como software de pré-lançamento, a Microsoft não dá suporte formal a ele.
> 
> 

## <a name="what-is-acs"></a>O que é o ACS?
A maioria dos desenvolvedores não são especialistas em identidade e geralmente não querem gastar tempo desenvolvendo a autenticação e mecanismos de autenticação para seus aplicativos e serviços. ACS é um serviço do Azure que fornece uma maneira fácil de autenticar usuários que precisam de tooaccess seus aplicativos web e serviços sem a necessidade de lógica de autenticação complexa toofactor em seu código.

Olá recursos a seguir está disponível no ACS:

* Integração com o Windows Identity Foundation (WIF).
* Suporte para IPs (provedores de identidade) populares da Web incluindo o Windows Live ID, o Google, o Yahoo e o Facebook.
* Suporte para o Serviço de Federação do Active Directory (AD FS) 2.0.
* Um Open Data Protocol (OData)-com base em serviço de gerenciamento que fornece acesso programático tooACS configurações.
* Um Portal de gerenciamento que permite o acesso administrativo toohello configurações do ACS.

Para obter mais informações sobre o ACS, consulte [Serviço de Controle de Acesso 2.0][Access Control Service 2.0].

## <a name="concepts"></a>Conceitos
Azure ACS baseia-se em entidades de saudação da identidade baseada em declarações - uma abordagem consistente toocreating os mecanismos de autenticação para aplicativos em execução no local ou na nuvem hello. Identidade baseada em declarações fornece uma maneira comum para aplicativos e serviços tooacquire as informações de identidade que precisam sobre os usuários de sua organização, em outras organizações e na Internet de saudação.

tarefas de saudação toocomplete neste guia, você deve compreender Olá conceitos a seguir:

**Cliente** -no contexto de saudação deste tooguide como, este é um navegador que está tentando o aplicativo web do toogain acesso tooyour.

**Aplicativo de terceira parte confiável (RP)** -aplicativo de um RP é um site ou serviço que terceirize a autoridade de autenticação tooone externo. Jargão de identidade, dizemos que Olá RP confia autoridade. Este guia explica como tooconfigure tootrust seu aplicativo ACS.

**Token** - um token é uma coleção de dados de segurança que geralmente são emitidos após a autenticação bem-sucedida de um usuário. Ele contém um conjunto de *declarações*, atributos de saudação autenticada do usuário. Uma declaração pode representar um nome de usuário, um identificador de uma função à qual um usuário pertence, a idade de um usuário e assim por diante. Um token é geralmente digitalmente assinado, que significa que sempre é tooits back originários de emissor e seu conteúdo não pode ser violado. Um usuário ganhos acesso tooa RP aplicativo apresentando um token válido emitido por uma autoridade de confiança do aplicativo de RP hello.

**IP (Provedor de Identidade)** - um IP é uma autoridade que autentica as identidades dos usuários e emite tokens de segurança. trabalho real Olá emitir tokens é implementado, embora um serviço especial chamado serviço de Token de segurança (STS). Exemplos típicos de IPs incluem o Windows Live ID, o Facebook, os repositórios de usuários de negócios (como o Active Directory) e assim por diante.
Quando o ACS é configurado tootrust um IP, sistema Olá aceitará e validará tokens emitidos por esse IP. ACS pode confiar em vários IPs de uma só vez, que significa que, quando seu aplicativo confia no ACS, você pode instantaneamente oferecer Olá de tooall seu aplicativo autenticada usuários Olá todos os IPs que ACS confia em seu nome.

**FP (Provedor de Federação)** - os IPs têm conhecimento direto dos usuários e os autenticam usando suas credenciais e emitem declarações sobre o que conhecem sobre eles. Um FP (provedor de federação) é um tipo diferente de autoridade: em vez de autenticar usuários diretamente, ele atua como um intermediário e agencia a autenticação entre um RP e um ou mais IPs. Tanto IPs quanto FPs emitem tokens de segurança, por isso ambos usam os STS (Serviços de Token de Segurança). O ACS é um FP.

**Mecanismo de regras do ACS** -regras de transformação de declarações de lógica de saudação tootransform usados tokens de entrada de tootokens de IPs confiáveis devem toobe consumida por Olá RP é codificada no formulário de simples. O ACS apresenta um mecanismo de regra que se encarrega de aplicar qualquer lógica de transformação que você especifique para seu RP.

**Namespace do ACS** - um namespace é uma partição de nível superior do ACS que você usa para organizar suas configurações. Um espaço para nome contém uma lista de IPs confiáveis, Olá RP aplicativos tooserve, regras de saudação que você espera Olá regra mecanismo tooprocess tokens de entrada e assim por diante. Um namespace expõe vários pontos de extremidade que serão usado pelo aplicativo hello e o desenvolvedor tooget ACS tooperform sua função.

Olá figura a seguir mostra como a autenticação do ACS funciona com um aplicativo web:

![Diagrama de fluxo do ACS][acs_flow]

1. Olá cliente (neste caso um navegador) solicita uma página do hello RP.
2. Desde que a solicitação de saudação ainda não foi autenticada, Olá RP redireciona autoridade Olá de toohello de usuário que ele confia, que é o ACS. Olá ACS apresenta Olá usuário escolha Olá de IPs que foram especificados para essa RP. usuário Olá seleciona IP apropriada hello.
3. Olá cliente procura a página de autenticação toohello endereços IP e solicita Olá usuário toolog em.
4. Depois Olá cliente é autenticado (por exemplo, são inseridas credenciais de identidade de saudação), Olá IP emite um token de segurança.
5. Depois de emitir um token de segurança, Olá IP redireciona Olá tooACS de cliente e cliente de Olá envia Olá token emitido por Olá tooACS IP.
6. ACS valida o token de segurança de saudação emitido pelo IP hello, entradas Olá identidade declarações nesse token em mecanismo de regras de saudação ACS, calcula Olá declarações de identidade de saída e emite um novo token de segurança que contém essas declarações de saída.
7. ACS redireciona Olá cliente toohello RP. cliente Olá envia Olá novo token de segurança emitido pelo ACS toohello RP. Olá RP valida a assinatura Olá Olá token de segurança emitido pelo ACS, valida Olá declarações nesse token e retorna Olá página originalmente solicitada.

## <a name="prerequisites"></a>Pré-requisitos
tarefas de saudação toocomplete neste guia, você precisará seguir Olá:

* Um JDK (Java Developer Kit) versão 1.6 ou posterior.
* Um IDE do Eclipse para desenvolvedores do Java EE, Indigo ou posterior. Isso pode ser baixado em <http://www.eclipse.org/downloads/>. 
* Uma distribuição de um servidor web baseado em Java ou servidor de aplicativo, como o Apache Tomcat, o GlassFish, o Servidor de Aplicativo JBoss ou o Jetty.
* Uma assinatura do Azure, que pode ser adquirida em <http://www.microsoft.com/windowsazure/offers/>.
* Olá Kit de ferramentas do Azure para Eclipse, abril de 2014 versão ou posterior. Para obter mais informações, consulte [Olá instalando o Kit de ferramentas do Azure para Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx).
* Um toouse do certificado x. 509 com o seu aplicativo. Você precisará desse certificado no certificado público (.cer) e no formato Troca de Informações Pessoais (.PFX). (As opções para criação desse certificado serão descritas posteriormente neste tutorial).
* Familiaridade com hello Azure computação emulador e implantação técnicas discutidas em [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx).

## <a name="create-an-acs-namespace"></a>Criar um namespace do ACS
toobegin usando o serviço de controle de acesso (ACS) no Azure, você deve criar um namespace do ACS. Olá namespace fornece um escopo exclusivo para endereçar recursos do ACS de dentro de seu aplicativo.

1. Faça logon no hello [Portal de gerenciamento][Azure Management Portal].
2. Clique em **Active Directory**. 
3. toocreate um novo namespace de controle de acesso, clique em **novo**, clique em **serviços de aplicativos**, clique em **controle de acesso**e, em seguida, clique em **criação rápida** . 
4. Insira um nome para o namespace de saudação. Azure verifica que esse nome hello é exclusivo.
5. Selecione Olá região na qual Olá namespace é usado. Para melhor desempenho de hello, use região Olá no qual você está implantando seu aplicativo.
6. Se você tiver mais de uma assinatura, selecione a assinatura de saudação que você deseja toouse para namespace Olá ACS.
7. Clique em **Criar**.

O Azure cria e ativa Olá namespace. Aguarde até que o status de saudação do hello novo namespace é **Active** antes de continuar. 

## <a name="add-identity-providers"></a>Adicionar provedores de identidade
Nesta tarefa, você pode adicionar IPs toouse com seu aplicativo RP para autenticação. Para fins de demonstração, esta tarefa mostra como tooadd Windows Live como um IP, mas você pode usar qualquer um dos Olá que IPS listado no Portal de gerenciamento do ACS de saudação.

1. Em Olá [Portal de gerenciamento][Azure Management Portal], clique em **do Active Directory**, selecione um namespace de controle de acesso e, em seguida, clique em **gerenciar**. Olá Portal de gerenciamento do ACS é aberto.
2. No painel de navegação esquerdo de saudação do hello Portal de gerenciamento do ACS, clique em **provedores de identidade**.
3. O Windows Live ID é habilitado por padrão e não pode ser excluído. Para fins deste tutorial, apenas o Windows Live ID é usado. Nessa tela, no entanto, é onde você pode adicionar outros IPs, clicando em Olá **adicionar** botão.

O Windows Live ID agora está habilitado como um IP para o seu namespace do ACS. Em seguida, você pode especificar o aplicativo web de Java (toobe criada posteriormente) como uma RP.

## <a name="add-a-relying-party-application"></a>Adicionar um aplicativo de terceira parte confiável
Nesta tarefa, você configurar ACS toorecognize o aplicativo web Java como um aplicativo válido do RP.

1. No Portal de gerenciamento do ACS de Olá, clique em **aplicativos de terceira parte**.
2. Em Olá **aplicativos de terceiros confiáveis** , clique em **adicionar**.
3. Em Olá **Adicionar aplicativo de terceiros confiável** página, Olá a seguir:
   
   1. Em **nome**, nome de tipo de saudação de saudação RP. Para fins desse tutorial, digite **Aplicativo Web do Azure**.
   2. Em **Modo**, selecione **Inserir as configurações manualmente**.
   3. Em **Realm**, tipo hello URI toowhich Olá token de segurança emitido pelo ACS se aplica. Para esta tarefa, digite **http://localhost:8080/**.
      ![Realm de terceira parte confiável para uso no emulador de computação][relying_party_realm_emulator]
   4. Em **URL de retorno** tipo hello URL toowhich ACS retorna o token de segurança de saudação. Para esta tarefa, digite **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![URL de retorno da terceira parte confiável para uso no emulador de computação][relying_party_return_url_emulator]
   5. Aceite valores padrão de saudação restante Olá dos campos de saudação.
4. Clique em **Salvar**.

Você agora configurou com êxito o aplicativo web Java quando ele é executado no emulador de computação do Azure hello (em http://localhost:8080 /) toobe uma RP em seu namespace do ACS. Em seguida, crie regras de saudação que o ACS usa declarações tooprocess para Olá RP.

## <a name="create-rules"></a>Criar regras
Nesta tarefa, defina regras de saudação que unidade como declarações são passadas do IPs tooyour RP. Para finalidade de saudação deste guia, simplesmente configuraremos valores e tipos de declaração de entrada do ACS toocopy Olá diretamente no token de saída de hello, sem filtrar ou modificá-los.

1. Na página principal do Portal de gerenciamento do ACS hello, clique em **grupos de regras**.
2. Em Olá **grupos de regras** , clique em **o grupo de regras padrão para o aplicativo Web do Azure**.
3. Em Olá **Editar grupo de regras** , clique em **gerar**.
4. Em Olá **gerar regras: grupo de regras padrão para o aplicativo Web do Azure** página, verifique se o Windows Live ID está marcada e, em seguida, clique em **gerar**.    
5. Em Olá **Editar grupo de regras** , clique em **salvar**.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>Carregar um namespace de ACS de tooyour de certificado
Nesta tarefa, você deve carregar um. Certificado PFX que será usado toosign solicitações de token criadas por seu namespace do ACS.

1. Na página principal do Portal de gerenciamento do ACS hello, clique em **certificados e chaves**.
2. Em Olá **certificados e chaves** , clique em **adicionar** acima **assinatura de Token**.
3. Em Olá **adicionar Token de assinatura de certificado ou chave** página:
   1. Em Olá **usado para** seção, clique em **aplicativo de terceiros confiável** e selecione **aplicativo Web do Azure** (que você tenha configurado como nome de saudação do seu aplicativo de terceira parte).
   2. Em Olá **tipo** seção, selecione **certificado x. 509**.
   3. Em Olá **certificado** seção, clique botão de procura hello e arquivo de certificado x. 509 toohello que você deseja toouse. Esse será um arquivo .PFX. Selecione o arquivo hello, clique em **abrir**e digite a senha do certificado Olá em Olá **senha** caixa de texto. Observe que, para fins de teste, você deve usar um certificado autoassinado. toocreate um certificado autoassinado, use Olá **novo** botão Olá **biblioteca de filtro ACS** diálogo (descrito adiante), ou use Olá **encutil.exe** utility do hello [site projeto] [ project website] de hello Azure Starter Kit para Java.
   4. Verifique se **Tornar Primário** está marcado. O **adicionar Token de assinatura de certificado ou chave** página deve ter aparência a seguir toohello semelhante.
       ![Adicionar certificado de autenticação de tokens][add_token_signing_cert]
   5. Clique em **salvar** toosave suas configurações e fechar Olá **adicionar Token de assinatura de certificado ou chave** página.

Em seguida, examine informações do Olá Olá integração de aplicativos página e cópia Olá URI que você precisará tooconfigure seu toouse de aplicativos Java web ACS.

## <a name="review-hello-application-integration-page"></a>Página de integração de aplicativos de saudação de revisão
Você pode encontrar todas as informações de saudação e Olá código necessário tooconfigure seu toowork Java web application (Olá aplicativo RP) com o ACS na página de integração de aplicativos de saudação do hello Portal de gerenciamento do ACS. Você precisará dessas informações ao configurar seu aplicativo web Java para autenticação federada.

1. No Portal de gerenciamento do ACS de Olá, clique em **integração de aplicativos**.  
2. Em Olá **integração de aplicativos** , clique em **páginas de logon**.
3. Em Olá **integração da página de logon** , clique em **aplicativo Web do Azure**.

Em Olá **integração da página de logon: aplicativo Web do Azure** página Olá URL listada nas **opção 1: página de logon hospedada no ACS tooan Link** será usado em seu aplicativo da web de Java. Esse valor será necessário quando você adiciona Olá filtro de serviços de controle de acesso do Azure biblioteca tooyour aplicativo Java.

## <a name="create-a-java-web-application"></a>Criar um aplicativo web Java
1. No Eclipse, no menu de saudação clique **arquivo**, clique em **novo**e, em seguida, clique em **projeto Web dinâmico**. (Se você não vir **projeto Web dinâmico** listado como um projeto disponível depois de clicar em **arquivo**, **novo**, em seguida, Olá a seguir: clique em **arquivo**, clique em **novo**, clique em **projeto**, expanda **Web**, clique em **projeto Web dinâmico**e clique em  **Em seguida**.) Para fins deste tutorial, nomeie o projeto de saudação **MyACSHelloWorld**. (Certifique-se de usar esse nome, as etapas subsequentes neste tutorial esperam sua toobe de arquivo WAR denominado MyACSHelloWorld). Sua tela será exibido a seguir toohello semelhante:
   
    ![Criar um Projeto Hello World para exemplo do ACS][create_acs_hello_world]
   
    Clique em **Concluir**.
2. Na exibição do Explorador de Projeto do Eclipse, expanda **MyACSHelloWorld**. Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.
3. Em Olá **novo arquivo JSP** caixa de diálogo, o arquivo de saudação do nome **index.jsp**. Manter a pasta pai Olá MyACSHelloWorld/WebContent, conforme mostrado na seguinte hello:
   
    ![Adicionar um arquivo JSP para exemplo do ACS][add_jsp_file_acs]
   
    Clique em **Avançar**.
4. Em Olá **Selecionar modelo JSP** caixa de diálogo, selecione **novo arquivo JSP (html)** e clique em **concluir**.
5. Quando o arquivo do hello index.jsp for aberto no Eclipse, adicionar no texto toodisplay **ACS Olá, mundo!** dentro de saudação existente `<body>` elemento. Seu atualizada `<body>` conteúdo deve aparecer da seguinte hello:
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    Salve o index.jsp.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Adicionar Olá tooyour aplicativo de biblioteca do filtro ACS
1. No explorador de Projeto do Eclipse, clique com o botão direito do mouse em **MyACSHelloWorld**, clique em **Caminho de Compilação** e em **Configurar Caminho de Compilação**.
2. Em Olá **caminho de compilação de Java** caixa de diálogo, clique em Olá **bibliotecas** guia.
3. Clique em **Adicionar Biblioteca**.
4. Clique em **Filtro dos Serviços de Controle de Acesso do Azure (da MS Open Tech)** e clique em **Avançar**. Olá **filtro de serviços de controle de acesso do Azure** caixa de diálogo é exibida.  (Olá **local** campo pode ter um caminho diferente, dependendo de onde você instalou o Eclipse, e o número de versão Olá poderia ser diferente, dependendo das atualizações de software.)
   
    ![Adicionar a biblioteca de filtros do ACS][add_acs_filter_lib]
5. Usando um navegador aberto toohello **integração da página de logon** página de hello Portal de gerenciamento, copiar Olá URL listado no hello **opção 1: página de logon hospedada no ACS Link tooan** campo e cole-o em Olá **o ponto de extremidade do ACS autenticação** campo da caixa de diálogo do hello Eclipse.
6. Usando um navegador aberto toohello **Editar aplicativo de terceiros confiável** página de hello Portal de gerenciamento, copiar Olá URL listado no hello **Realm** campo e cole-o em Olá **terceira parte confiável Realm**  campo da caixa de diálogo do hello Eclipse.
7. Dentro de saudação **segurança** seção da caixa de diálogo de Eclipse da saudação, se você quiser toouse um certificado existente, clique em **procurar**, navegar toohello certificado você deseja toouse, selecione-o e clique em  **Abra**. Ou, se você quiser toocreate um novo certificado, clique em **novo** toodisplay Olá **novo certificado** caixa de diálogo, em seguida, especifique a senha Olá, nome do arquivo. cer de saudação e nome do arquivo. pfx Olá Olá novo certificado.
8. Verificar **certificado de saudação de inserção no arquivo WAR de saudação**. Certificado Olá incorporação dessa maneira inclui-lo em sua implantação sem exigir que você toomanually adicioná-lo como um componente. (Se, em vez disso, você deve armazenar o certificado externamente do seu arquivo WAR, você pode adicionar o certificado hello como um componente de função e desmarque **certificado de saudação de inserção no arquivo WAR de saudação**.)
9. [Opcional] Mantenha a opção **Requer conexões HTTPS** marcada. Se você definir essa opção, você precisará tooaccess seu aplicativo usando o protocolo HTTPS de saudação. Se você não quiser toorequire conexões de HTTPS, desmarque essa opção.
10. Para uma implantação toohello compute emulator, seu **Azure ACS filtro** configurações serão a aparência a seguir toohello semelhante.
    
    ![Configurações de filtro ACS do Azure para uma implantação toohello o emulador de computação][add_acs_filter_lib_emulator]
11. Clique em **Concluir**.
12. Clique em **Sim** quando for apresentada uma caixa de diálogo informando que será criado um arquivo web.xml.
13. Clique em **Okey** tooclose Olá **caminho de compilação de Java** caixa de diálogo.

## <a name="deploy-toohello-compute-emulator"></a>Implantar o emulador de computação toohello
1. No Explorador de Projeto do Eclipse, clique com o botão direito do mouse em **MyACSHelloWorld**, clique em **Azure** e em **Pacote para Azure**.
2. Para **Nome do Projeto**, digite **MyAzureACSProject** e clique em **Avançar**.
3. Selecione um JDK e o servidor de aplicativo. (Essas etapas são abordadas detalhadamente em Olá [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tutorial).
4. Clique em **Concluir**.
5. Clique em Olá **executar no emulador do Azure** botão.
6. Depois que o aplicativo web Java for iniciado no emulador de computação hello, feche todas as instâncias do seu navegador (de forma que qualquer sessão de navegador atual não interferir com o teste de logon do ACS).
7. Execute seu aplicativo ao abrir <http://localhost:8080/MyACSHelloWorld/> em seu navegador (ou <https://localhost:8080/MyACSHelloWorld/> se tiver selecionado **Requer conexões HTTPS**). Você deve ser solicitado para um logon do Windows Live ID e, em seguida, você deve ser levado toohello URL de retorno especificado para o aplicativo de terceira parte.
8. Quando terminar de exibir o aplicativo, clique em Olá **redefinir emulador do Azure** botão.

## <a name="deploy-tooazure"></a>Implantar tooAzure
toodeploy tooAzure, você precisará toochange Olá terceira parte confiável realm URL de retorno e de seu namespace do ACS.

1. Dentro de saudação Portal de gerenciamento do Azure, em Olá **Editar aplicativo de terceiros confiável** , modifique **Realm** toobe Olá URL do seu site implantado. Substituir **exemplo** com o nome DNS Olá especificado para sua implantação.
   
    ![Realm de terceira parte confiável para uso na produção][relying_party_realm_production]
2. Modificar **URL de retorno** toobe Olá URL do seu aplicativo. Substituir **exemplo** com o nome DNS Olá especificado para sua implantação.
   
    ![URL de retorno da terceira parte confiável para uso na produção][relying_party_return_url_production]
3. Clique em **salvar** toosave seu atualizado respondem parte realm URL de retorno e alterações.
4. Lembre-Olá **integração da página de logon** página aberta no navegador, será necessário toocopy-lo em breve.
5. No explorador de Projeto do Eclipse, clique com o botão direito do mouse em **MyACSHelloWorld**, clique em **Caminho de Compilação** e em **Configurar Caminho de Compilação**.
6. Clique em Olá **bibliotecas** , clique em **filtro de serviços de controle de acesso do Azure**e, em seguida, clique em **editar**.
7. Usando um navegador aberto toohello **integração da página de logon** página de hello Portal de gerenciamento, copiar Olá URL listado no hello **opção 1: página de logon hospedada no ACS Link tooan** campo e cole-o em Olá **o ponto de extremidade do ACS autenticação** campo da caixa de diálogo do hello Eclipse.
8. Usando um navegador aberto toohello **Editar aplicativo de terceiros confiável** página de hello Portal de gerenciamento, copiar Olá URL listado no hello **Realm** campo e cole-o em Olá **terceira parte confiável Realm**  campo da caixa de diálogo do hello Eclipse.
9. Dentro de saudação **segurança** seção da caixa de diálogo de Eclipse da saudação, se você quiser toouse um certificado existente, clique em **procurar**, navegar toohello certificado você deseja toouse, selecione-o e clique em  **Abra**. Ou, se você quiser toocreate um novo certificado, clique em **novo** toodisplay Olá **novo certificado** caixa de diálogo, em seguida, especifique a senha Olá, nome do arquivo. cer de saudação e nome do arquivo. pfx Olá Olá novo certificado.
10. Manter **certificado de saudação de inserção no arquivo WAR de saudação** marcada, supondo que você deseja tooembed Olá certificado no arquivo WAR de saudação.
11. [Opcional] Mantenha a opção **Requer conexões HTTPS** marcada. Se você definir essa opção, você precisará tooaccess seu aplicativo usando o protocolo HTTPS de saudação. Se você não quiser toorequire conexões de HTTPS, desmarque essa opção.
12. Para uma implantação tooAzure, as configurações de filtro do Azure ACS procurará a seguir toohello semelhante.
    
    ![Configurações do Filtro do ACS do Azure para uma implantação de produção][add_acs_filter_lib_production]
13. Clique em **concluir** tooclose Olá **Editar biblioteca** caixa de diálogo.
14. Clique em **Okey** tooclose Olá **propriedades MyACSHelloWorld** caixa de diálogo.
15. No Eclipse, clique em Olá **publicar tooAzure nuvem** botão. Responder a prompts toohello, semelhantes a como feito no hello **toodeploy tooAzure seu aplicativo** seção Olá [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tópico. 

Depois que seu aplicativo da web foi implantado, feche todas as sessões de navegador aberto, executar o aplicativo da web e você deverá toosign com as credenciais do Windows Live ID, seguido por envio toohello URL do seu aplicativo de terceira parte de retorno.

Quando você terminar usando o aplicativo Hello World do ACS, lembre-se de implantação de saudação toodelete (você pode aprender como toodelete uma implantação em Olá [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tópico).

## <a name="next_steps"></a>Próximas etapas
Para um exame de saudação SAML Security Assertion Markup Language () retornado pelo aplicativo de tooyour do ACS, consulte [como tooview SAML retornado pelo hello Azure Access Control Service][How tooview SAML returned by hello Azure Access Control Service]. toofurther explorar tooexperiment com cenários mais sofisticados e funcionalidade do ACS, consulte [Access Control Service 2.0][Access Control Service 2.0].

Além disso, essa saudação de exemplo usado **certificado de saudação de inserção no arquivo WAR de saudação** opção. Essa opção facilita o certificado de saudação toodeploy simples. Se em vez disso, você deseja tookeep seu certificado de autenticação separado do seu arquivo WAR, você pode usar o hello técnica a seguir:

1. Dentro de saudação **segurança** seção Olá **filtro de serviços de controle de acesso do Azure** caixa de diálogo, digite **${env. JAVA_HOME}/mycert.cer** e desmarque **certificado de saudação de inserção no arquivo WAR de saudação**. (Ajuste mycert.cer se o nome do arquivo do certificado for diferente). Clique em **concluir** caixa de diálogo tooclose hello.
2. Certificado de saudação cópia como um componente em sua implantação: no Explorador de projeto do Eclipse, expanda **MyAzureACSProject**, clique com botão direito **WorkerRole1**, clique em **propriedades** , expanda **função do Azure**e clique em **componentes**.
3. Clique em **Adicionar**.
4. Dentro de saudação **adicionar componente** caixa de diálogo:
   
   1. Em Olá **importação** seção:
      1. Saudação de uso **arquivo** botão toonavigate toohello certificado toouse. 
      2. Para **Método**, selecione **copiar**.
   2. Para **nome como**, clique na caixa de texto de saudação e aceite o nome padrão de saudação.
   3. Em Olá **implantar** seção:
      1. Para **Método**, selecione **copiar**.
      2. Para **toodirectory**, tipo **JAVA_HOME %**.
   4. O **adicionar componente** caixa de diálogo deve ser a seguir toohello semelhante.
      
       ![Adicionar componente de certificado][add_cert_component]
   5. Clique em **OK**.

Neste ponto, seu certificado seria incluído em sua implantação. Observe que independentemente de você insere certificado Olá no arquivo WAR de saudação ou adicioná-lo como uma implantação de tooyour do componente, você precisa tooupload Olá certificado tooyour namespace conforme descrito em Olá [carregar um namespace de ACS de tooyour certificado] [ Upload a certificate tooyour ACS namespace] seção.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

