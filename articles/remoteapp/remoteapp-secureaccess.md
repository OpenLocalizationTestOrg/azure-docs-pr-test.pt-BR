---
title: aaaSecuring acesso tooAzure RemoteApp e superiores | Microsoft Docs
description: Saiba como proteger acesso tooAzure RemoteApp usando acesso condicional no Active Directory do Azure
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>Protegendo o acesso tooAzure RemoteApp e posterior
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Neste artigo, forneceremos uma visão geral de como um administrador pode configurar um canal de acesso seguro a partir do usuário final do hello, por meio do RemoteApp do Azure e terminando com um recurso seguro, como um banco de dados SQL ou outro aplicativo de back-end. meta de saudação é toomake-se de que somente usuários autorizados Olá reunião desejado condições podem acessar aplicativos remotos, e que Olá back-end seguro só podem ser acessados do ambiente do Azure RemoteApp Olá controlado e não de outros locais.

Há 3 áreas principais Olá administrador precisa toolook em:

![Considerações de acesso condicional do RemoteApp do Azure](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Continue lendo para perguntas de toothese informações e respostas.

## <a name="who-can-access-hello-collection"></a>Quem pode acessar a coleção de Olá?
administrador de saudação escolhe usuários Olá que podem acessar aplicativos remotos na coleção de saudação. Você pode usar as contas corporativas ou de estudante do Azure AD (Azure Active Directory) – anteriormente chamadas de "contas organizacionais" – ou as contas da Microsoft (por exemplo, @outlook.com). A maioria dos cenários de empresa usam contas do AD do Azure; Eles permitem que você use recursos de acesso condicional discutidos posteriormente e também são a única opção Olá para coleções de domínio. restante de saudação do artigo Olá pressupõe que você está usando contas do AD do Azure com o Azure RemoteApp.

**O que conseguimos:**

Usando o AD do Azure contas toocontrol acesso tooAzure que RemoteApp fornece duas coisas:

1. Sempre sabemos quem pode acessar Olá aplicativos que publicou e acessar qualquer back-ends esses aplicativos se conectem.
2. Podemos controlar Olá subjacente do AD do Azure para criar e excluir contas de usuário, definir políticas de senha, usam a autenticação multifator, etc. 

## <a name="how-is-hello-collection-accessed-from-where"></a>Como a coleção de saudação é acessada? De onde?
Normalmente, os administradores querem toodefine políticas para acessar um ambiente voltado para a Internet público, como o Azure RemoteApp. Por exemplo, quiserem tooensure que os usuários que acessam o ambiente de saudação de fora da rede corporativa Olá tenham acesso de toogain de autenticação multifator (MFA) de toouse; ou, talvez eles devem ser bloqueados completamente.

Administradores do RemoteApp do Azure podem usar a funcionalidade de saudação disponível por meio de políticas de acesso condicional do Azure AD Premium tooset para seu ambiente do Azure RemoteApp. Eles também podem usar relatórios avançados e alertas toomonitor recursos como o ambiente de hello está sendo acessado.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>Como tooset o acesso condicional para o Azure RemoteApp
Estamos toowalk contínuo por meio de um cenário de exemplo – administrador do Azure RemoteApp Olá quer tooblock ambiente de toohello de acesso quando os usuários estiverem fora da rede corporativa hello.

> [!NOTE]
> Vamos supor que você atualizou o AD do Azure toohello camada Premium e que você tenha criado pelo menos uma coleção do RemoteApp do Azure.
> 
> 

1. No portal do Azure, clique em Olá **do Active Directory** guia. Clique em diretório Olá ser tooconfigure.
   
   Lembre-se: O acesso condicional é uma propriedade do seu diretório e não do Azure RemoteApp para que toda a configuração é feita no nível do diretório de saudação. Isso também significa que você precisa toobe Olá directory administrador toomake essas alterações.
2. Clique em **aplicativos**e, em seguida, clique em **RemoteApp do Microsoft Azure** tooset o acesso condicional. Observe que é possível configurar o acesso condicional para cada aplicativo de “software como serviço” no diretório separadamente.
   ![Configurar o acesso condicional para o RemoteApp do Azure](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Em Olá **configurar** guia, defina **habilitar regras de acesso** tooON.
   ![Habilitar regras de acesso para o RemoteApp do Azure](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. Você pode configurar várias regras e escolha quem tooapply para:
   
   1. Escolha **bloquear acesso quando não estiver no trabalho** toocompletely impedir que os usuários acessem o Azure RemoteApp fora do ambiente de rede Olá você especificar.
   2. Clique em opção Olá abaixo toodefine Olá intervalos de endereços IP que constituem sua "rede confiável". Tudo que estiver fora será rejeitado.
5. Teste sua configuração iniciando o cliente do Azure RemoteApp Olá de um endereço IP fora do intervalo de saudação especificado. Depois de entrar com as suas credenciais do AD do Azure, você verá uma mensagem como esta:

![Acesso negado tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Recursos de acesso condicional futuros
equipe do Active Directory do Azure de saudação está trabalhando em novas capacidades de acesso condicional. Os administradores serão toocreate capaz de novos tipos de regras além de regras de localização com base em rede. Visualização pública da nova funcionalidade de saudação deve estar disponível em breve.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Como toomonitor acessar tooAzure RemoteApp
Toouse um ótimo recurso junto com acesso condicional é a funcionalidade de relatório de Azure Active Directory Premium Olá. Você pode usar toomonitor relatórios quem está acessando o seu ambiente e detectar qualquer atividade suspeita.

Por exemplo, você pode ver os nomes de saudação de usuários Olá quem acessou o Azure RemoteApp, quantas vezes o fizeram e quando.

1. No portal do Azure, clique em **Active Directory**e em seu diretório.
2. Vá toohello **relatórios** guia.
3. Saudação de relatórios, selecione lista **uso do aplicativo** em **integrado a aplicativos**.
   
   Você verá algumas estatísticas agregadas para o Azure RemoteApp. 
   ![Estatísticas de acesso agregadas do Azure RemoteApp](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Clique em Olá aplicativo tooreveal informações sobre os usuários que acessam o Azure RemoteApp.
   ![Estatísticas de acesso do usuário para o Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Resumo
Com o Azure Active Directory Premium, você pode definir o acesso regras tooAzure RemoteApp (e outros software como um aplicativo de serviço disponível por meio do AD do Azure). Regras são atualmente limitado toonetwork diretivas de localização com base, mas serão no futuro de saudação estendidas tooother aspectos do gerenciamento corporativo.

O Azure AD Premium também oferece a emissão de relatórios e monitoramento de recursos que estendem mais Olá controle Olá administrador tem sobre seu ambiente do Azure RemoteApp.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>Como garanto que meu recurso seguro seja acessível somente a partir de meu ambiente do RemoteApp do Azure?
Nas seções anteriores deste artigo com um foco sobre como proteger o ambiente do access toohello Azure RemoteApp. Podemos ter realizado que escolhendo os usuários de saudação que têm permissão de acesso e configurando o controle de toofurther de regras de acesso como eles podem usar o serviço de saudação.

Um cenário comum para implantações do Azure RemoteApp é que aplicativos remotos Olá necessário toocommunicate com um recurso de back-end, por exemplo um banco de dados SQL. Este recurso é hospedado no local (por exemplo, em uma rede corporativa) ou na nuvem de saudação (por exemplo, no Azure IaaS). Os administradores frequentemente querem toomake-se de que recursos de back-end Olá só podem ser acessados por aplicativos implantados por meio do RemoteApp do Azure e não por exemplo, por um aplicativo em execução diretamente no computador do usuário e acessar a Internet pública. O Azure RemoteApp geralmente é visto como Olá-gerenciadas centralmente e ambiente protegido e, portanto, somente o caminho Olá por meio do qual os usuários devem interagir com hello recursos de back-end.

solução de saudação é tooplace ambos hello Azure RemoteApp ambiente e recurso seguro Olá Olá VNET do Azure Virtual Network (). Se o recurso de saudação estiver em um site diferente, você pode estabelecer uma conexão VPN site a site, por exemplo, toocreate um rede virtual abrangência Olá data center do Azure e ambiente de local do cliente hello.

O RemoteApp do Azure oferece suporte a dois tipos de implantações de coleção onde você pode fornecer sua própria VNET:

* Não ingressaram no domínio: Olá aplicativos terão "linha de visão" de saudação outros recursos em redes de saudação. Por exemplo, isso pode ser usado tooconnect aplicativos tooa banco de dados SQL que usa a autenticação do SQL (aplicativos autenticar usuário Olá diretamente no banco de dados de saudação)
* Domínio: máquinas virtuais de saudação usadas pelo RemoteApp do Azure são tooa ingressado no controlador de domínio Olá VNET. Isso é útil quando aplicativos Olá necessitam tooauthenticate em um controlador de domínio do Windows em recursos de back-end do pedido tooget acesso tooa.
  ![Uma coleção de domínios do Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>Como toocreate uma conexão segura entre o Azure e meu ambiente local
Há várias opções de configuração para conectar seus ambientes do Azure e local. Uma boa visão geral das opções de saudação está disponível aqui.

Com o Azure RemoteApp necessário tooconfigure sua VNet primeiro e, em seguida, usá-lo durante o processo de criação de saudação da sua coleção. 

## <a name="hello-complete-solution"></a>solução completa de saudação
diagrama de Olá abaixo mostra a solução completa de saudação onde, criamos um canal de proteger o acesso do usuário final de hello, por meio do Azure RemoteApp (ARA), em recursos de back-end de saudação.
![Proteger o Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) na etapa 1, Olá usuários selecionados e criar regras de acesso que controlam como o ARA pode ser acessado. No exemplo hello abaixo que só é permitido acesso para os usuários que trabalham na rede corporativa hello. Os usuários não compatível não será em todos os tooaccess capaz de ambiente de ARA de saudação.
Na fase 2 nós expôs recursos de back-end Olá somente por meio da configuração de rede virtual/VPN Olá que podemos controlar. O Azure RemoteApp foi colocado em Olá mesmo VNet. resultado final de saudação é recurso Olá só pode ser acessado por meio do ambiente de ARA hello.

