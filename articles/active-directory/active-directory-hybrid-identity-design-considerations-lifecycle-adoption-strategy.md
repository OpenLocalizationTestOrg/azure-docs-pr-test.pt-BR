---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar a estratégia de adoção de ciclo de vida de identidade híbrida | Microsoft Docs"
description: "Ajuda a definir tarefas de gerenciamento de identidade híbrida Olá toohello opções disponíveis para cada fase do ciclo de vida de acordo com."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Determinar uma estratégia de adoção para o ciclo de vida da identidade híbrida
Nesta tarefa, você definirá a estratégia de gerenciamento de identidade Olá para seu híbrida identidade solução toomeet Olá requisitos de negócios que você definiu no [determinar as tarefas de gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

toodefine Olá híbrida identidade tarefas de gerenciamento de acordo com o ciclo de vida de identidade de ponta a ponta toohello apresentado anteriormente nesta etapa, terá tooconsider Olá opções disponíveis para cada fase do ciclo de vida.

## <a name="access-management-and-provisioning"></a>Provisionamento e gerenciamento de acesso
Com uma solução de gerenciamento de acesso de conta válida, sua organização pode controlar com precisão quem tem acesso toowhat informações da organização hello.

O controle de acesso é uma função essencial de um sistema centralizado e de ponto único de provisionamento. Além de proteger informações confidenciais, os controles de acesso revelam as contas existentes cujas autorizações não são aprovadas ou não são mais necessárias. contas de toocontrol obsoleto, Olá informações de provisionamento sistema links conta juntos com autoridade informações sobre usuários de saudação que possuem contas de saudação. Informações de identidade de usuário autoritativo normalmente são mantidas em bancos de dados hello e diretórios de recursos humanos.

Contas em empresas de TI sofisticados incluem centenas de parâmetros que definem autoridades Olá, e esses detalhes podem ser controladas pelo sistema de provisionamento. Novos usuários podem ser identificados com dados Olá fornecidas fonte autoritativa hello. funcionalidade de aprovação de solicitação de acesso de saudação inicia processos Olá aprovarem (ou rejeitam) recursos de provisionamento para eles.

| Fase de gerenciamento do ciclo de vida | No local | Nuvem | Híbrido |
| --- | --- | --- | --- |
| Provisionamento e gerenciamento de contas |Usando a função de servidor de serviços de domínio do Active Directory® (AD DS) hello, você pode criar uma infraestrutura escalável, segura e gerenciável para gerenciamento de usuários e recursos e oferecem suporte para aplicativos habilitados por diretório, como o Microsoft® Exchange Server. <br><br> [Você pode provisionar grupos no AD DS por meio de um gerenciador de identidades](https://technet.microsoft.com/library/ff686261.aspx) <br>[ Você pode provisionar usuários no AD DS](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Os administradores podem usar o controle de acesso toomanage usuário acessar tooshared recursos para fins de segurança. No Active Directory, o controle de acesso é administrado no nível de objeto Olá por definir diferentes níveis de acesso ou permissões, tooobjects, como controle total, gravação, leitura ou sem acesso. O controle de acesso no Active Directory determina como os usuários podem usar os objetos do Active Directory. Por padrão, as permissões em objetos do Active Directory são definidas configuração mais segura de toohello. |Você tem toocreate uma conta para todos os usuários que terão acesso a um serviço de nuvem da Microsoft. Você também pode alterar as contas de usuário ou excluí-las quando elas não forem mais necessárias. Por padrão, os usuários não têm permissões de administrador, mas, opcionalmente, você pode atribuí-las. Para obter mais informações, veja [Gerenciando usuários no AD do Azure](active-directory-create-users.md). <br><br> No Active Directory do Azure, um dos principais recursos de saudação é Olá capacidade toomanage acesso tooresources. Esses recursos podem fazer parte do diretório hello, como no caso de saudação de objetos de toomanage permissões por meio de funções no diretório de hello, ou recursos de diretório toohello externo, como aplicativos SaaS, os serviços do Azure e sites do SharePoint ou no local recursos. <br><br> No Olá solução de gerenciamento de acesso do centro do Azure do Active Directory é o grupo de segurança hello. proprietário do recurso de saudação (ou o administrador de saudação do diretório Olá) pode atribuir tooprovide um grupo um determinados recursos de toohello direito acesso que eles possuem. membros de saudação do grupo de saudação terão acesso hello e proprietário do recurso Olá pode delegar a lista de membros de Olá Olá toomanage à direita de uma pessoa – como um gerente de departamento ou um administrador de assistência técnica de toosomeone de grupo<br> <br> Gerenciando grupos de saudação tópico do AD do Azure fornece mais informações sobre como gerenciar o acesso por meio de grupos. |Estender identidades do Active Directory para a nuvem Olá por meio de sincronização e a federação |

## <a name="role-based-access-control"></a>Controle de acesso baseado em função
Controle de acesso baseado em função (RBAC) usa funções e políticas tooevaluate de provisionamento, testar e impor seus processos de negócios e regras para conceder acesso toousers. Os principais administradores criar políticas de provisionamento e atribuir usuários tooroles e que definem conjuntos de tooresources de direitos para essas funções. RBAC estende Olá identidade solução toouse baseada em software processos de gerenciamento e reduzir a interação manual no processo de provisionamento de saudação do usuário.
RBAC do AD do Azure permite que a quantidade de saudação do hello da empresa toorestrict de operações que um indivíduo pode fazer depois que ele tem acesso tooAzure Portal de gerenciamento. Usando o portal do RBAC toocontrol acesso toohello, abordagens de administradores de TI ca de acesso delegado usando Olá gerenciamento de acesso a seguir:

* **Atribuição de função com base em grupo**: você pode atribuir acesso tooAzure AD grupos que podem ser sincronizados do seu Active Directory local. Isso permite que você tooleverage Olá investimentos existentes que sua organização tornou-se em ferramentas e processos para gerenciar os grupos. Você também pode usar o recurso de gerenciamento de grupo delegado de saudação do Azure AD Premium.
* **Aproveite criado em funções no Azure**: você pode usar três funções — tooensure proprietário e colaborador leitor, usuários e grupos têm permissão toodo somente Olá tarefas precisam toodo seus trabalhos.
* **Acesso granular tooresources**: você pode atribuir funções toousers e grupos para uma assinatura específica, grupo de recursos ou um recurso individual do Azure como um site ou o banco de dados. Dessa forma, você pode garantir que os usuários tenham acesso tooall Olá os recursos necessários e nenhum tooresources de acesso que eles não precisam de toomanage.

## <a name="provisioning-and-other-customization-options"></a>Provisionamento e outras opções de personalização
Sua equipe pode usar toodecide planos e requisitos de negócios quanto solução de identidade toocustomize hello. Por exemplo, uma grande empresa pode exigir um plano de distribuição em fases para fluxos de trabalho e adaptadores personalizados com base em uma linha do tempo para o provisionamento incremental de aplicativos que são amplamente usados entre regiões geográficas. Outro plano de personalização pode fornecer para dois ou mais toobe aplicativos provisionados em toda a organização, após o teste com êxito. A interação do usuário de aplicativo pode ser personalizada e procedimentos para o provisionamento de recursos podem ser alterado tooaccommodate automatizada de provisionamento.

Você pode cancelar o provisionamento tooremove um serviço ou componente. Por exemplo, o desprovisionamento uma conta significa que conta Olá é excluída de um recurso.

modelo híbrido de saudação do provisionamento de recursos combina a solicitação e abordagens baseadas em função, que são suportadas pelo AD do Azure. Para um subconjunto de funcionários ou sistemas gerenciados, uma empresa pode desejar tooautomate acesso com a atribuição baseada em função. A empresa pode também querer lidar com todas as outras solicitações ou exceções de acesso por meio de um modelo baseado em solicitação. Algumas empresas podem começar usando atribuições manuais e evoluir no sentido de um modelo híbrido, visando uma implantação totalmente baseada em função no futuro.

Outras empresas podem ser impraticável para negócios motivos tooachieve completa baseada em função de provisionamento e o destino uma abordagem híbrida como uma meta desejada. Ainda outras empresas podem ser atendidas com somente baseado em solicitação de provisionamento e não deseja tooinvest esforço adicional toodefine e gerenciar políticas de provisionamento automatizadas, baseado em função.

## <a name="license-management"></a>Gerenciamento de licenças
Gerenciamento de licença baseada em grupo no AD do Azure permite que os administradores a atribuir o grupo de segurança usuários tooa e AD do Azure automaticamente atribui licenças tooall membros de saudação do grupo de saudação. Se um usuário subsequentemente é adicionado ou removido do grupo de saudação, uma licença serão automaticamente atribuída ou removida conforme apropriada.

Use grupos de sincronização do AD local ou gerencie-os no AD do Azure. Associação isso com o Azure AD premium gerenciamento de grupo de autoatendimento poderá facilmente delegar tomadores de decisão apropriada de toohello de atribuição de licença. Você vai garantir que os problemas relacionados a conflitos de licenças e dados de localização ausentes sejam classificados automaticamente.

## <a name="self-regulating-user-administration"></a>Administração autoreguladora de usuários
Quando sua organização começar tooprovision recursos em todas as organizações internas, você implementar o recurso de administração de usuário autorregulador Olá. Você pode obter vantagens hello e os benefícios de provisionamento de usuários entre limites organizacionais. Nesse ambiente, uma alteração no status de um usuário se reflete automaticamente nos direitos de acesso em regiões geográficas e limites da organização. Você pode reduzir os custos de provisionamento e simplificar processos de aprovação e acesso de saudação. implementação de saudação percebe que todo o potencial de implementação de controle de acesso baseado em função para o gerenciamento de acesso de ponta a ponta em sua organização hello. Reduza os custos administrativos por meio de procedimentos automatizados para controlar o provisionamento de usuários. Você pode aprimorar a segurança automatizando a aplicação de políticas de segurança, além de simplificar e centralizar o gerenciamento do ciclo de vida do usuário e o provisionamento de recursos para grandes grupos de usuários.

> [!NOTE]
> Para saber mais, veja o tópico Configurando o AD do Azure para o gerenciamento de acesso a aplicativos por autoatendimento
> 
> 

Os Serviços do AD do Azure baseados em licença (baseados em direito) funcionam ativando uma assinatura no locatário de serviço/diretório do AD do Azure. Depois de saudação assinatura está ativa recursos de serviço de saudação podem ser gerenciados por administradores de serviço de diretório/e usados por usuários licenciados. Para saber mais, consulte o tópico Como funciona o licenciamento do AD do Azure?
Integração com outros provedores de terceiros

Active Directory do Azure fornece logon único e avançado aplicativo toothousands de segurança de acesso de aplicativos SaaS e aplicativos da web locais. Para obter uma lista detalhada de galeria de aplicativos do Active Directory do Azure para aplicativos SaaS com suporte, consulte a lista de compatibilidade de Federação do Active Directory do Azure: provedores de identidade de terceiros que podem ser usado tooimplement o logon único

## <a name="define-synchronization-management"></a>Definir o gerenciamento de sincronização
A integração de seus diretórios locais ao AD do Azure torna os usuários mais produtivos ao fornecer uma identidade comum para acesso aos recursos na nuvem e locais. Com essa integração usuários e organizações podem aproveitar seguinte hello:

* As organizações podem fornecer aos usuários uma identidade híbrida comum entre locais ou serviços baseados em nuvem aproveita o Active Directory do Windows Server e, em seguida, conectando-se tooAzure do Active Directory.
* Os administradores podem fornecer acesso condicional com base no recurso do aplicativo, na identidade de usuário e dispositivo, no local de rede e na autenticação multifator.
* Os usuários podem aproveitar sua identidade comuns por meio de contas no AD do Azure tooOffice 365, Intune, aplicativos SaaS e aplicativos de terceiros.
* Os desenvolvedores podem criar aplicativos que utilizam o modelo de identidade comum hello, integração de aplicativos em locais do Active Directory ou do Azure para aplicativos baseados em nuvem

Olá figura a seguir apresenta um exemplo de uma exibição de alto nível do processo de sincronização de identidade.

![](./media/hybrid-id-design-considerations/identitysync.png)

Processo de sincronização de identidades

Saudação de revisar as opções de sincronização de saudação de toocompare tabela a seguir:

| Opção de gerenciamento de sincronização | Vantagens | Desvantagens |
| --- | --- | --- |
| Com base em sincronização (através do DirSync ou do AADConnect) |Usuários e grupos sincronizados no local e na nuvem  <br>  **Controle de política**: políticas de conta podem ser definidas por meio do Active Directory, que fornece Olá administrador Olá capacidade toomanage as políticas de senha, estação de trabalho, restrições, controles de bloqueio e mais, sem ter que tooperform adicional tarefas na nuvem de saudação.  <br>  **Controle de acesso**: pode restringir o acesso toohello serviço em nuvem para que, Olá serviços podem ser acessados por meio do ambiente corporativo hello, por meio de servidores online, ou ambos. <br>  Menos chamadas de suporte: se os usuários tiverem menos tooremember de senhas, eles são menos provável tooforget-los. <br>  Segurança: Informações e identidades de usuário são protegidas porque todos os servidores de saudação e serviços usados no logon único, são dominados e controlados localmente. <br>  Suporte para autenticação forte: você pode usar autenticação forte (também chamada de autenticação de dois fatores) com o serviço de nuvem hello. No entanto, se usar esse recurso, você deve usar o logon único. | |
| Com base em federação (através do AD FS) |Habilitado pelo serviço de token de segurança (STS). Quando você configura um STS tooprovide único acesso de logon com um serviço de nuvem da Microsoft, você estará criando uma confiança federada entre seu STS local e domínio federado hello, que você especificou no seu locatário do AD do Azure. <br> Permite que os usuários finais toouse Olá mesmo conjunto de credenciais tooobtain acessar toomultiple os recursos <br>os usuários finais não tem toomaintain vários conjuntos de credenciais. Ainda, Olá possuem tooprovide tooeach suas credenciais uma saudação participantes recursos., B2B e B2C cenários com suporte. |Requer profissionais especializados para implantação e manutenção de servidores dedicados do AD FS local. Há restrições no uso de saudação da autenticação forte se você planejar toouse do AD FS para os STS. Para saber mais, consulte o artigo [Configurando opções avançadas do AD FS 2.0](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Para saber mais, veja o artigo [Integrando identidades locais com o Active Directory do Azure](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Consulte também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

