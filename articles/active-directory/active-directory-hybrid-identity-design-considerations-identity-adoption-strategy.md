---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - definir uma estratégia de adoção de identidade híbrida | Microsoft Docs"
description: "Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas hello, que você escolhe ao autenticar usuário hello e antes de permitir acesso toohello aplicativo. Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Definir uma estratégia de adoção de identidade híbrida
Nesta tarefa, você definirá estratégia de adoção do hello híbrida identidade para seu híbrida identidade solução toomeet Olá requisitos de negócios que foram abordados:

* [Determinar as necessidades de negócios](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Determinar os requisitos de sincronização de diretório](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Determinar os requisitos de autenticação multifator](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>Definir uma estratégia para as necessidades de negócios
tarefa de primeiro Olá endereços determinar necessidades de negócios de organizações de saudação.  Isso é muito amplo e pode não atender aos objetivos, se você não atuar com precisão.  No início de saudação manter a simplicidade, mas lembre-se sempre tooplan para um design que acomodar e facilitar a alteração no hello futuras.  Independentemente de ser um extremamente complexo ou um design simples, o Active Directory do Azure é Olá Microsoft Identity plataforma dá suporte ao Office 365, Microsoft Online Services e aplicativos com reconhecimento de nuvem.

## <a name="define-an-integration-strategy"></a>Definir uma estratégia de integração
A Microsoft tem três cenários básicos de integração: as identidades de nuvem, as identidades sincronizadas e as identidades federadas.  Planeje a adoção de uma dessas estratégias de integração.  Olá estratégia que você escolher pode variar e incluir decisões Olá na escolha de um, o tipo de experiência do usuário que você deseja tooprovide, têm alguns Olá infraestrutura local já e o que é mais econômico de hello.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

cenários de saudação definidos no hello acima figura são:

* **Identidades de nuvem**: essas são as identidades que existem apenas na nuvem de saudação.  No caso de saudação do AD do Azure, eles reside especificamente no seu diretório do AD do Azure.
* **Sincronizado**: essas são as identidades que existem no local e na nuvem hello.  Com o Azure AD Connect, os usuários são criados ou associados a contas existentes do AD do Azure.  Olá hash da senha do usuário é sincronizado por meio Olá local ambiente toohello nuvem no que é chamado um hash de senha.  Quando sincronizados usando uma limitação de saudação é que se um usuário está desabilitado no ambiente local de Olá, pode levar backup too3 horas para que tooshow de status da conta no AD do Azure.  Isso é devido toohello intervalo de tempo de sincronização.
* **Federado**: essas identidades existem no local e na nuvem hello.  Com o Azure AD Connect, os usuários são criados ou associados a contas existentes do AD do Azure.  

> [!NOTE]
> Para obter mais informações sobre opções de sincronização de saudação [integrando suas identidades locais ao Active Directory do Azure](connect/active-directory-aadconnect.md).
> 
> 

Olá a tabela a seguir ajudará a determinar Olá vantagens e desvantagens cada Olá estratégias a seguir:

| Estratégia | Vantagens | Desvantagens |
| --- | --- | --- |
| **Identidades de nuvem** |Toomanage mais fácil para a organização de pequena porte. <br> Nada é necessário hardware adicional do tooinstall não no local<br>Facilmente desabilitada se o usuário Olá deixa a empresa Olá |Os usuários deverão toosign-in ao acessar as cargas de trabalho na nuvem Olá <br> Senhas podem ou não ser Olá mesmo para identidades de nuvem e local |
| **Identidades sincronizadas** |As senhas locais são autenticadas nos diretórios locais e na nuvem  <br>Toomanage mais fácil para organizações de pequenas, médias ou grandes <br>Os usuários podem usar SSO (Logon único) para alguns recursos <br> Método preferido da Microsoft para sincronização <br> Toomanage mais fácil |Alguns clientes podem estar relutante toosynchronize seus diretórios com hello nuvem devido a política da empresa específico |
| **Federado** |Os usuários podem fazer SSO  <br>Se um usuário é encerrado ou deixa, conta de Olá pode ser desabilitada imediatamente e acesso revogado,<br> Tem suporte para cenários avançados que não podem ser realizados com identidades sincronizadas |Mais etapas toosetup e configurar <br> Maior manutenção <br> Pode exigir hardware adicional para a infraestrutura de STS Olá <br> Pode exigir um servidor de Federação adicionais de hardware tooinstall hello. Software adicional será necessário se o AD FS é usado <br> Requer configuração ampla para SSO <br> Crítico o ponto de falha se o servidor de Federação Olá estiver inativo, os usuários não serão possível tooauthenticate |

### <a name="client-experience"></a>Experiência do cliente
estratégia de saudação que você usar ditará experiência de entrada do usuário de saudação.  Olá tabelas a seguir fornecem informações sobre quais usuários Olá devem esperar a sua entrada experiência toobe.  Observe que nem todos os provedores de identidades federadas tem suporte para todos os cenários de SSO.

**Aplicativos de rede privada ou ingressados no domínio**:

|  | Identidade sincronizada | Identidade federada |
| --- | --- | --- |
| Navegadores da Web |Autenticação baseada em formulários |o logon único, às vezes necessário toosupply ID da organização |
| Outlook |Solicita credenciais |Solicita credenciais |
| Skype for Business (Lync) |Solicita credenciais |logon único para o Lync, solicitação de credenciais para o Exchange |
| Skydrive Pro |Solicita credenciais |logon único |
| Assinatura do Office Pro Plus |Solicita credenciais |logon único |

**Fontes externas ou não confiáveis**:

|  | Identidade sincronizada | Identidade federada |
| --- | --- | --- |
| Navegadores da Web |Autenticação baseada em formulários |Autenticação baseada em formulários |
| Outlook, Skype for Business (Lync), Skydrive Pro, assinatura do Office |Solicita credenciais |Solicita credenciais |
| Exchange ActiveSync |Solicita credenciais |logon único para o Lync, solicitação de credenciais para o Exchange |
| Aplicativos móveis |Solicita credenciais |Solicita credenciais |

Se você tiver determinado da tarefa 1 que você tenha um 3ª parte toouse contínuo de IdP ou são uma federação tooprovide com o AD do Azure, você precisa de recursos de suporte toobe atento Olá a seguir:

* Qualquer provedor de SAML 2.0 que é compatível com hello perfil SP-Lite pode dar suporte a autenticação tooAzure AD e aplicativos associados
* Autenticação passiva dá suporte a, que facilita a autenticação tooOWA, SPO, etc.
* Os clientes Exchange Online podem ter suporte por meio de saudação perfil de cliente avançado (ECP) do SAML 2.0

Conheça também os recursos que não estão disponíveis:

* Sem o suporte a WS-Trust/Federação, todos os outros clientes ativos ficarão inoperantes
  * Isso significa que nenhum cliente do Lync, o cliente do OneDrive, assinatura do Office, Office Mobile anterior tooOffice 2016
* Transição de autenticação do Office toopassive permitirão toosupport IdPs de 2.0 SAML puro, mas o suporte ainda estará em uma base por cliente

> [!NOTE]
> Para Olá lista mais atualizada de leitura Olá artigo http://aka.ms/ssoproviders.
> 
> 

## <a name="define-synchronization-strategy"></a>Definir uma estratégia de sincronização
Nesta tarefa, você definirá as ferramentas de saudação que serão local dados toohello na nuvem usado toosynchronize Olá organização e o que topologia, você deve usar.  Porque, a maioria das organizações usa o Active Directory, informações sobre o uso do Azure AD Connect tooaddress Olá perguntas sobre acima são fornecidas em detalhes.  Para ambientes que não têm o Active Directory, há informações sobre como usar o FIM 2010 R2 ou o MIM 2016 toohelp planejar essa estratégia.  No entanto, as versões futuras do Azure AD Connect dará suporte a diretórios LDAP, dependendo de sua linha do tempo, essas informações podem ser capaz de tooassist.

### <a name="synchronization-tools"></a>Ferramentas de sincronização
Ao longo de anos de hello, várias ferramentas de sincronização tem existia e usada para vários cenários.  No momento do Azure AD Connect é Olá vá tootool ideal para todos os cenários com suporte.  O AAD Sync e o DirSync continuam disponíveis e podem fazer parte do seu ambiente imediatamente. 

> [!NOTE]
> Para Olá informações mais recentes sobre os recursos de saudação com suporte de cada ferramenta, leia [comparação das ferramentas de integração de diretórios](active-directory-hybrid-identity-design-considerations-tools-comparison.md) artigo.  
> 
> 

### <a name="supported-topologies"></a>Topologias com suporte
Ao definir uma estratégia de sincronização, topologia Olá usado deve ser determinada. Dependendo Olá informações determinado na etapa 2, você pode determinar qual topologia são Olá toouse adequada de um. floresta única Hello, única topologia do AD do Azure é hello mais comuns e consiste em uma única floresta do Active Directory e uma única instância do AD do Azure.  Isso será usado na maioria dos cenários de saudação do toobe e é a topologia de saudação esperada ao usar a instalação do Azure AD conectar Express conforme mostrado na figura abaixo a saudação.

![](./media/hybrid-id-design-considerations/single-forest.png)Única floresta cenário é muito comum para organizações de grande e pequeno o mesmo toohave várias florestas, conforme mostrado na Figura 5.

> [!NOTE]
> Para obter mais informações sobre Olá local diferente e topologias do AD do Azure com a sincronização do Azure AD Connect leia o artigo de saudação [topologias para Azure AD Connect](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Cenário de topologia de várias florestas

Se esse caso de Olá Olá, em seguida, multi-forest único topologia do AD do Azure deve ser considerada se hello itens a seguir forem verdadeiras:

* Os usuários têm apenas 1 identidade em todas as florestas – Olá identificando exclusivamente a seção usuários abaixo descreve isso mais detalhadamente.
* usuário Olá autentica toohello floresta em que sua identidade está localizada
* O UPN e a âncora de origem (ID imutável) serão gerados nessa floresta.
* Todas as florestas são acessíveis pelo Azure AD Connect – isso significa que ele não precisa toobe integrado ao domínio e pode ser colocado em uma rede de Perímetro, se isso facilita isso.
* Os usuários têm apenas uma caixa de correio.
* floresta de saudação que hospeda a caixa de correio do usuário tem a melhor qualidade de dados Olá para atributos visíveis na lista de endereços Global (GAL) Exchange de saudação
* Se não há nenhuma caixa de correio no usuário hello, então qualquer floresta pode ser usado toocontribute esses valores
* Se você tiver uma caixa de correio vinculada, em seguida, também há outra conta toosign uma floresta diferente usada no.

> [!NOTE]
> Objetos que existem em ambos os locais e na nuvem Olá estão "conectados" através de um identificador exclusivo. Olá o contexto de sincronização de diretórios, este identificador exclusivo é tooas chamado hello SourceAnchor. No contexto de saudação do logon único, isso é chamado tooas Olá imutável. [Conceitos de design para o Azure AD Connect](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) para obter mais considerações sobre o uso de saudação do SourceAnchor.
> 
> 

Se Olá acima não forem verdadeiras e você tiver mais de uma conta ativa ou a mais de uma caixa de correio, o Azure AD Connect escolher uma e ignorar Olá outros.  Se você vincular caixas de correio, mas nenhuma outra conta, essas contas não será exportado tooAzure AD e esse usuário não é um membro de grupos.  Isso é diferente de como ele estava em Olá anteriores com o DirSync e é intencional toobetter suporte esses cenários de várias florestas. Um cenário de várias floresta é mostrado na figura de saudação abaixo.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Cenário de várias florestas do AD do Azure**

É recomendável suportada toohave que apenas um único diretório no AD do Azure para uma organização, mas é que uma relação de 1:1 é mantida entre um servidor de sincronização do Azure AD Connect e um diretório do AD do Azure.  Você vai precisar de uma instalação do Azure AD Connect para cada instância do AD do Azure.  Além disso, o AD do Azure, por design é isolado e usuários em uma instância do AD do Azure não será capaz de toosee usuários em outra instância.

É possível e tooconnect com suporte, uma instância de diretórios do AD do Azure do Active Directory toomultiple conforme mostrado na figura abaixo a saudação local:

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Cenário de filtragem de floresta única**

Ordem toodo seguir Olá deve ser verdadeira:

* Os servidores de sincronização do Azure AD Connect devem ser configurados para filtragem para que cada um deles tenha um conjunto de objetos mutuamente exclusivos.  Isso feito, por exemplo, definir o escopo de cada domínio específico do servidor tooa ou unidade Organizacional.
* Um domínio DNS só pode ser registrado em um único diretório do AD do Azure para Olá UPNs dos usuários Olá Olá AD deve usar namespaces separados ao local
* Os usuários em uma instância do AD do Azure só será capaz de toosee usuários de sua instância.  Não ser capaz de toosee usuários Olá outras instâncias
* Somente um dos diretórios de saudação do AD do Azure pode habilitar o Exchange híbrido com hello AD local
* Exclusividade mútua também se aplica a toowrite-back.  Isso faz com que alguns recursos de write-back não sejam compatíveis com esta topologia, pois eles supõem a existência de uma única configuração local.  Isso inclui:
  * Agrupar write-back com configuração padrão
  * Write-back de dispositivo

Lembre-se de que o seguinte Olá não tem suporte e não deve ser escolhido como uma implementação:

* Não é suportada toohave vários servidores de sincronização do Azure AD Connect conectando toohello mesmo Azure AD directory mesmo que eles estejam configurado toosynchronize mutuamente definidos do objeto
* Não há suporte para toosync Olá diretórios de toomultiple AD do Azure do mesmo usuário. 
* Também é toomake sem suporte, uma alteração de configuração toomake usuários em um tooappear do AD do Azure como contatos em outro diretório do AD do Azure. 
* Também é diretórios do toomodify sem suporte do Azure AD Connect sincronização tooconnect toomultiple AD do Azure.
* Diretórios do AD do Azure são isolados por padrão. É configuração do hello toochange sem suporte do Azure AD Connect tooread de dados de sincronização de outro diretório do AD do Azure em um toobuild tentativa um GAL comum e unificado entre diretórios hello. Também é tooexport sem suporte por usuários como contatos tooanother AD usando a sincronização do Azure AD Connect no local.

> [!NOTE]
> Se sua organização restringe computadores na sua rede de conexão toohello da Internet, este artigo lista os pontos de extremidade de saudação (FQDNs, IPv4 e IPv6 intervalos de endereços) que você deve incluir na sua saída permite listas e Internet Explorer zona de Sites confiáveis do cliente computadores tooensure seus computadores com êxito podem usar o Office 365. Para saber mais, leia o artigo [Intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Definir uma estratégia de autenticação multifator
Nesta tarefa, você definirá Olá toouse de estratégia de autenticação multifator.  O Azure Multi-Factor Authentication é fornecido em duas versões distintas.  Um é um baseado em nuvem e outros Olá baseado usando Olá servidor Azure MFA local.  Com base na avaliação de saudação que você anteriormente, você pode determinar qual solução é Olá um correto para sua estratégia.  Use a tabela de saudação abaixo toodetermine opção de design que melhor atender os requisitos de segurança da sua empresa:

Opções de design de vários fatores:

| Ativo toosecure | MFA na nuvem Olá | MFA local |
| --- | --- | --- |
| Aplicativos da Microsoft |sim |sim |
| Aplicativos SaaS na Galeria de aplicativo hello |sim |sim |
| Aplicativos IIS publicados por meio da Proxy de aplicativo do Azure AD |sim |sim |
| Aplicativos do IIS não publicados por meio de saudação Proxy de aplicativo do Azure AD |não |sim |
| Acesso remoto, como VPN e RDG |não |sim |

Embora você talvez estabeleceu uma solução para sua estratégia, ainda precisará de avaliação de saudação toouse acima de onde estejam localizados os usuários.  Isso pode causar Olá solução toochange.  Use tabela Olá abaixo tooassist você para determinar isso:

| Local do usuário | Opção de design preferida |
| --- | --- |
| Azure Active Directory |Multi-FactorAuthentication na nuvem Olá |
| Azure AD e AD local usando federação com AD FS |Ambos |
| AD do Azure e AD local usando o Azure AD Connect sem sincronização de senha |Ambos |
| O AD do Azure e o AD local usando o Azure AD Connect com sincronização de senha |Ambos |
| AD local |Servidor Multi-Factor Authentication |

> [!NOTE]
> Você também deve garantir que opção Olá de design de autenticação multifator que você selecionou dá suporte a recursos de saudação que são necessários para seu design.  Para obter mais informações, leia [escolha a solução de segurança de vários fatores de saudação para você](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Provedor de Multi-Factor Authentication
A autenticação multifator está disponível por padrão para administradores globais que tenham um locatário do Active Directory do Azure. No entanto, se você deseja tooextend tooall de autenticação multifator dos seus usuários e/ou deseja tooyour administradores globais toobe tootake capaz de aproveitar os recursos, como o portal de gerenciamento hello, saudações personalizadas e relatórios, em seguida, você deve comprar e configurar Provedor de autenticação multifator.

> [!NOTE]
> Você também deve garantir que opção Olá de design de autenticação multifator que você selecionou dá suporte a recursos de saudação que são necessários para seu design. 
> 
> 

## <a name="next-steps"></a>Próximas etapas
[Determinar os requisitos para proteção de dados](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Confira também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

