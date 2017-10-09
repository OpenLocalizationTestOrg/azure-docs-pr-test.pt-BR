---
title: "aaaAzure acesso e identidade práticas recomendadas de segurança | Microsoft Docs"
description: "Este artigo fornece um conjunto de práticas recomendadas para gerenciamento de identidade e controle de acesso usando recursos internos do Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Práticas recomendadas de Gerenciamento de Identidade do Azure e segurança de controle de acesso
Muitos considerem toobe Olá novo limite camada de identidade para segurança, assumir essa função perspectiva Olá tradicionais baseados na rede. Essa evolução de pivot principal de saudação para atenção de segurança e investimentos provenientes de fato Olá perímetro da rede se tornaram cada vez mais porosas e essa defesa do perímetro não pode ser tão eficaz como costumavam toohello anterior explosão de [BYOD](http://aka.ms/byodcg) dispositivos e aplicativos de nuvem.

Neste artigo, discutiremos um conjunto de práticas recomendadas de segurança de controle de acesso e gerenciamento de identidade do Azure. Essas práticas recomendadas são derivadas da nossa experiência com [AD do Azure](../active-directory/active-directory-whatis.md) e experiências de saudação de clientes, como por conta própria.

Para cada prática recomendada, vamos explicar:

* A prática recomendada que Olá é
* Por que você deseja tooenable essa prática recomendada
* O que pode ser resultado de saudação se você não a prática recomendada de saudação tooenable
* Prática recomendada de toohello possíveis alternativas
* Como você pode aprender a prática recomendada de saudação tooenable

Esse gerenciamento de identidades do Azure de controle de acesso artigo sobre práticas recomendadas se baseia em uma opinião consenso e recursos da plataforma Azure e conjuntos de recursos de segurança que existem em tempo de saudação que este artigo foi escrito. Tecnologias e opiniões alterar ao longo do tempo e este artigo será atualizado em um tooreflect regularmente essas alterações.

As práticas recomendadas de segurança de controle de acesso e gerenciamento de identidade do Azure discutidas neste artigo incluem:

* Centralizar o gerenciamento de identidade
* Habilitar SSO (Logon Único)
* Implantar o gerenciamento de senhas
* Impor MFA (autenticação multifator) para usuários
* Usar RBAC (controle de acesso baseado em função)
* Controlar os locais em que os recursos são criados usando o gerenciador de recursos
* Os desenvolvedores de guia tooleverage recursos de identidade para aplicativos SaaS
* Monitorar ativamente as atividades suspeitas

## <a name="centralize-your-identity-management"></a>Centralizar o gerenciamento de identidade
Uma etapa importante para proteger sua identidade é tooensure que a TI pode gerenciar as contas de um único local sobre onde essa conta foi criada. Enquanto a maioria Olá das empresas Olá as organizações de TI terá sua conta primária de diretório local, implantações de nuvem híbrida são no aumento de saudação e é importante entender como toointegrate locais e diretórios na nuvem e forneça um experiência perfeita toohello ao usuário final.

tooaccomplish isso [identidade híbrida](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) cenário recomendamos duas opções:

* Sincronizar seu diretório local com seu diretório na nuvem usando o Azure AD Connect
* Federar sua identidade local com seu diretório de nuvem usando [Serviços de Federação do Active Directory](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS)

As organizações que não toointegrate que suas identidades locais com sua identidade de nuvem terão aumentado administrativas sobrecarga no gerenciamento de contas, o que aumenta a probabilidade de saudação de erros e violações de segurança.

Para obter mais informações sobre a sincronização do AD do Azure, leia o artigo Olá [integrando suas identidades locais ao Active Directory do Azure](../active-directory/active-directory-aadconnect.md).

## <a name="enable-single-sign-on-sso"></a>Habilitar SSO (Logon Único)
Quando você tiver vários toomanage de diretórios, isso se torna um problema administrativo não apenas para equipe de TI, mas também para usuários finais que terá tooremember várias senhas. Usando [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) você dará aos usuários a capacidade Olá Olá use mesmo conjunto de credenciais em toosign e acessar recursos de saudação que eles precisam, independentemente onde esse recurso está localizado no local ou na nuvem hello.

Usar o SSO tooenable usuários tooaccess seus [aplicativos SaaS](../active-directory/active-directory-appssoaccess-whatis.md) com base em sua conta organizacional no AD do Azure. Isso é aplicável não apenas a aplicativos de SaaS da Microsoft, mas também a outros aplicativos, como [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) e [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md). Seu aplicativo pode ser configurado toouse AD do Azure como um [identidade baseada em SAML](../active-directory/fundamentals-identity.md) provedor. Como um controle de segurança do AD do Azure não emitirá um token que permite que eles toosign em aplicativo hello, a menos que receberam acesso usando o Azure AD. Você pode conceder acesso diretamente ou por meio de um grupo do qual eles fazem parte.

> [!NOTE]
> Olá decisão toouse SSO terá impacto sobre como integrar seu diretório local com seu diretório na nuvem. Se você quiser SSO, você precisará toouse federação, porque a sincronização de diretório somente fornecerá [mesma experiência de logon](../active-directory/active-directory-aadconnect.md).
>
>

As organizações que não impõem SSO para seus usuários e aplicativos são mais tooscenarios exposto em que os usuários terão várias senhas que aumenta a probabilidade de saudação de reutilização de senhas ou usar senhas de usuários diretamente.

Você pode aprender mais sobre o Azure AD SSO lendo o artigo Olá [gerenciamento do AD FS e personalização com o Azure AD Connect](../active-directory/active-directory-aadconnect-federation-management.md).

## <a name="deploy-password-management"></a>Implantar o gerenciamento de senhas
Em cenários em que você tiver vários locatários ou tooenable usuários muito[redefinir suas próprias senhas](../active-directory/active-directory-passwords-update-your-own-password.md), é importante que você use abuso de tooprevent de políticas de segurança apropriadas. No Azure, você pode aproveitar o recurso de redefinição de senha de autoatendimento hello e personalizar toomeet de opções de segurança Olá seus requisitos de negócios.

Ele é particularmente importante tooobtain comentários desses usuários e aprender com suas experiências conforme eles tentam tooperform essas etapas. Com base nessas experiências, elaborar um plano toomitigate possíveis problemas que podem ocorrer durante a implantação de saudação para um grupo maior. Também é recomendável que você use Olá [relatório de atividade de registro de redefinição de senha](../active-directory/active-directory-passwords-get-insights.md) usuários de saudação toomonitor que estão sendo registrado.

As organizações que desejam tooavoid senha alterar chamadas de suporte, mas habilitar os usuários tooreset suas próprias senhas são mais suscetíveis tooa superior chamada volume toohello técnico devido a problemas de toopassword. Em organizações que têm vários locatários, é essencial que você implementa esse tipo de recurso e habilitar os usuários tooperform redefinição dentro dos limites de segurança que foram estabelecidos na política de segurança de saudação.

Você pode aprender mais sobre a redefinição de senha ao ler o artigo Olá [Implantando o gerenciamento de senhas e treinamento usuários toouse-](../active-directory/active-directory-passwords-best-practices.md).

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>Impor MFA (autenticação multifator) para usuários
Para organizações que precisam toobe compatíveis com os padrões do setor, como [PCI DSS versão 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), autenticação multifator é um deve ter a capacidade de autenticar os usuários. Além de estar em conformidade com os padrões do setor, impor os usuários do MFA tooauthenticate também pode ajudar a tipo de roubo de credenciais organizações toomitigate de ataque, como [Pass-the-Hash (PtH)](http://aka.ms/PtHPaper).

Ativando o Azure MFA para os usuários, você está adicionando uma segunda camada de segurança toouser entradas e transações. Nesse caso, uma transação pode ser o acesso a um documento localizado em um servidor de arquivos ou no SharePoint Online. MFA do Azure também ajuda a probabilidade de saudação do IT tooreduce que uma credencial comprometida terá dados do access tooorganization.

Por exemplo: impor o MFA do Azure para seus usuários e configurá-lo toouse uma chamada telefônica ou mensagem de texto como a verificação. Se as credenciais do usuário Olá estiverem comprometidas, o invasor Olá não ser capaz de tooaccess qualquer recurso porque ele não terá telefone do acesso toouser. As organizações que não adiciona camadas extras de proteção de identidade são mais suscetíveis de ataque de roubo de credenciais, que pode causar o comprometimento de toodata.

Uma alternativa para organizações que desejam tookeep Olá autenticação completa controle local foi toouse [servidor Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), também chamado de MFA no local. Usando esse método, você ainda será tooenforce capaz de autenticação de vários fatores, mantendo Olá MFA server local.

Para obter mais informações sobre o Azure MFA, leia o artigo Olá [guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Usar RBAC (controle de acesso baseado em função)
Restringindo o acesso com base em Olá [necessário tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) princípios de segurança é fundamental para as organizações que desejam tooenforce políticas de segurança para acesso a dados. Controle de acesso do Azure baseado em função (RBAC) pode ser usado tooassign permissões toousers, grupos e aplicativos em um determinado escopo. escopo de saudação de uma atribuição de função pode ser uma assinatura, um grupo de recursos ou um único recurso.

Você pode aproveitar [interna do RBAC](../active-directory/role-based-access-built-in-roles.md) funções no Azure tooassign toousers de privilégios. Considere o uso de *colaborador da conta de armazenamento* para operadores de nuvem que precisam de contas de armazenamento toomanage e *Colaborador clássico de conta de armazenamento* contas de armazenamento clássicas toomanage de função. Operadores de nuvem que precisa toomanage VMs e conta de armazenamento, considere a possibilidade de adicioná-los muito*colaborador da máquina Virtual* função.

As organizações que não impõem o controle de acesso de dados, aproveitando os recursos como RBAC podem ser fornecendo mais privilégios de usuários tootheir necessário. Isso pode causar o comprometimento de toodata por permitir o acesso de usuários toocertain tipos de tipos de dados (por exemplo, alto impacto nos negócios) que eles não deveriam ter em primeiro lugar de saudação.

Você pode aprender mais sobre o RBAC do Azure ao ler o artigo Olá [o controle de acesso](../active-directory/role-based-access-control-configure.md).

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>Controlar os locais em que os recursos são criados usando o gerenciador de recursos
Habilitar tarefas de tooperform de operadores de nuvem enquanto impedindo recentes convenções que são necessárias toomanage recursos da sua organização é muito importante. As organizações que desejam locais de saudação toocontrol onde os recursos são criados devem codificar esses locais.

tooachieve isso, as organizações podem criar políticas de segurança que têm definições que descrevem as ações de saudação ou recursos que são especificamente negados. Você atribuir essas definições de política no escopo de saudação desejado, como assinatura hello, grupo de recursos ou um recurso individual.

> [!NOTE]
> Isso não é Olá mesmo como RBAC, ele utiliza, na verdade, usuários de saudação do RBAC tooauthenticate que tem o privilégio toocreate esses recursos.
>
>

Aproveite [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) políticas personalizadas de toocreate também para cenários onde Olá organização deseja tooallow operações apenas quando Olá Centro de custo apropriado estiver associado; caso contrário, eles negará a solicitação de saudação.

As organizações que não estão controlando como os recursos são criados são mais suscetíveis toousers que pode ofender serviço Olá criando mais recursos que precisam. Proteger o processo de criação do recurso de saudação é toosecure uma etapa importante um cenário de vários locatários.

Você pode aprender mais sobre como criar políticas com o Azure Resource Manager lendo o artigo Olá [recursos de toomanage de política de uso e controlar o acesso](../azure-resource-manager/resource-manager-policy.md).

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>Os desenvolvedores de guia tooleverage recursos de identidade para aplicativos SaaS
A identidade do usuário será aproveitada em muitos cenários, quando os usuários acessam [aplicativos de SaaS](https://azure.microsoft.com/marketplace/active-directory/all/) que pode ser integrados ao diretório local ou na nuvem. Primeiramente, é recomendável que os desenvolvedores usam toodevelop uma metodologia proteger esses aplicativos, como [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx). O Azure AD simplifica a autenticação para os desenvolvedores fornecendo identidade como um serviço, com suporte para protocolos de padrão do setor, como [OAuth 2.0](http://oauth.net/2/) e [OpenID Connect](http://openid.net/connect/), bem como bibliotecas de software livre para plataformas diferentes.

Verifique se tooregister qualquer aplicativo que terceirize a autenticação tooAzure AD, este é um procedimento obrigatório. Olá motivo é porque o AD do Azure precisa a comunicação com o aplicativo hello Olá toocoordinate ao tratamento sign-on (SSO) ou troca de tokens. sessão de usuário de saudação expira quando o tempo de vida de saudação do hello token emitido pelo AD do Azure expire. Sempre avalie se o aplicativo deve usar esse tempo ou se você pode reduzir o tempo. Tempo de vida de saudação reduzindo pode agir como uma medida de segurança que força os usuários toosign out com base em um período de inatividade.

As organizações que não impõem aplicativos de tooaccess de controle de identidade não guia e seus desenvolvedores sobre como toosecurely integrar aplicativos com o seu sistema de gerenciamento de identidade podem ser mais suscetível tipo de roubo de toocredential de ataque, como [fraca autenticação e gerenciamento de sessão descrito na parte superior do projeto de segurança de aplicativo de Web aberta (OWASP) 10](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).

Você pode saber mais sobre cenários de autenticação para aplicativos de SaaS lendo [Cenários de autenticação do Azure AD](../active-directory/active-directory-authentication-scenarios.md).

## <a name="actively-monitor-for-suspicious-activities"></a>Monitorar ativamente as atividades suspeitas
De acordo com muito[relatório de violação de dados 2016 Verizon](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), comprometimento de credenciais ainda está em aumento hello e tornando-se uma das empresas mais lucrativas Olá criminosos virtuais. Por esse motivo, é importante toohave um sistema de monitor de identidade ativa que pode detectar atividades suspeitas do comportamento e disparar um alerta para investigação futura rapidamente. O Azure AD tem dois recursos principais que podem ajudar as organizações a monitorar suas identidades: os [relatórios de anomalias](../active-directory/active-directory-view-access-usage-reports.md) do Azure AD Premium e a funcionalidade de [proteção de identidade](../active-directory/active-directory-identityprotection.md) do Azure AD.

Verifique se toouse Olá anomalias relatórios tooidentify tentativas toosign em [sem rastreamento](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [força bruta](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) ataques contra uma conta específica, toosign tentativas em vários locais, entrar de [infectados dispositivos](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) e endereços IP suspeitos. Lembre-se de que esses são relatórios. Em outras palavras, você deve ter processos e procedimentos em colocar para IT admins toorun esses relatórios diariamente hello ou sob demanda (geralmente em um cenário de resposta a incidentes).

Em contrapartida, proteção de identidade do AD do Azure é um sistema de monitoramento ativo e ele marcará riscos de saudação atual em seu próprio painel. Além disso, você também receberá notificações diárias de resumo por email. É recomendável que você ajustar o nível de risco de saudação de acordo com tooyour requisitos de negócios. nível de risco de saudação de um evento de risco é uma indicação (alto, médio ou baixo) de severidade de saudação do evento de risco hello. nível de risco de saudação ajuda os usuários a proteção de identidade priorizar ações Olá devem assumir organização de tootheir tooreduce Olá risco.

As organizações que não monitoram ativamente os seus sistemas de identidade estão em risco de ter as credenciais de usuários comprometidas. Sem o conhecimento que estão aproveitando as atividades suspeitas colocar usando essas credenciais, as organizações não será capaz de toomitigate esse tipo de ameaça.
Você pode saber mais sobre a proteção de identidade do Azure lendo [Proteção de Identidade do Azure Active Directory](../active-directory/active-directory-identityprotection.md).
