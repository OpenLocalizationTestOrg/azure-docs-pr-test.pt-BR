---
title: dados pessoais de aaaProtect com controles de acesso e identidade do Azure | Microsoft Docs
description: "Usando toohelp de controles de acesso e identidade do Azure que você proteja seus dados pessoais"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory e Autenticação Multifator: proteger dados pessoais com controles de acesso e identidade

Este artigo fornece informações e procedimentos que você pode usar dados pessoais de tooprotect usando os serviços e recursos de segurança do Active Directory do Azure e multi-factor authentication.

## <a name="scenario"></a>Cenário

Uma empresa cruzeiro grandes, com sede Olá dos Estados Unidos, está expandindo suas roteiros de toooffer operações Mediterrâneo hello, Adriatic e mares báltico, bem como Olá Britânicas. toosupport os esforços adquiriu várias linhas de cruzeiro menores na Itália, Alemanha, Dinamarca e hello UK 

empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello. Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes. Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais. linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.

Os funcionários corporativos acesso Olá rede da empresa Olá escritórios remotos e agentes espalhados Olá, mundo têm acesso toosome recursos da empresa.

## <a name="problem-statement"></a>Problema declarado

empresa Olá deve proteger a privacidade de saudação dos dados pessoais dos funcionários e clientes contra invasores que buscam toouse comprometido identidades toogain acesso. Eles também devem garantir que toopersonal de acesso a dados por usuários legítimos é restrito a somente aqueles que precisam de toodo seus trabalhos.

## <a name="company-goal"></a>Meta da empresa

a meta da empresa Olá é tooensure que acessam dados toopersonal é estritamente controlada. É essencial que as identidades de usuários com dados do access toopersonal ser protegidas por autenticação forte. Uma política de [privilégio mínimo] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) devem ser impostas para que os usuários legítimos único nível de saudação de acesso necessário e nada mais.

## <a name="solutions"></a>Soluções

Microsoft Azure fornece ferramentas de gerenciamento de identidade e acesso toohelp empresas controlar acesso tooresources que contêm dados pessoais.

### <a name="azure-active-directory"></a>Azure Active Directory

[Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/) (AAD) gerencia identidades e controla o acesso tooAzure bem como outros locais e outros recursos de nuvem, dados e aplicativos. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ajuda os administradores do Azure toominimize Olá várias pessoas têm acesso toocertain informações como dados pessoais. Ele permite toodiscover, restringir e monitorar seus tooresources e tooassign temporário, Just-in-(JIT) direitos administrativos tooeligible usuários de acesso e de identidades com privilégios. Também fornece informações sobre aqueles que têm privilégios administrativos do AAD.

atividades de saudação envolvidas usando AAD PIM incluem:

- Habilitar o Privileged Identity Management no diretório

- Usando informações importantes do Privileged Identity Management admin painel toosee em um relance

- Gerenciamento de identidades com privilégios de saudação (administradores) adicionando ou removendo a função de tooeach administradores permanentes ou qualificados

- Definindo configurações de ativação de função hello

- Ativar funções

- Examinar a atividade de função

#### <a name="how-do-i-enable-aad-pim"></a>Como fazer para habilitar o AAD PIM?

toostart usando PIM para seu diretório, Olá a seguir:

1. Entre em toohello portal do Azure como um administrador global do seu diretório.

2. Se sua organização tiver mais de um diretório, selecione seu nome de usuário no canto superior direito de saudação do hello portal do Azure. Selecione o diretório de saudação onde você usará o Azure AD Privileged Identity Management.

3. Selecione **mais serviços** e usar Olá **filtro** toosearch da caixa de texto para o Azure AD Privileged Identity Management.

4. Verificar **Pin toodashboard** e, em seguida, clique em **criar**. Olá aplicativo Privileged Identity Management é aberto.

Depois de configurar o Azure AD Privileged Identity Management, você verá blade de navegação Olá sempre que você abrir o aplicativo hello.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Para obter mais informações e instruções sobre como começar a usar o AAD PIM, consulte [Começar a usar o Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)

### <a name="azure-role-based-access-control"></a>Controle de Acesso Baseado em Função do Azure

[Controle de acesso baseado em função do Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ajuda a administradores do Azure gerenciar acesso tooAzure recursos habilitando o Olá concessão de acesso baseado em função do usuário hello. Você pode separar tarefas dentro de uma equipe e conceder apenas Olá total acesso toousers, grupos e aplicativos que precisam tooperform seus trabalhos.

Acesso baseado em função pode ser concedido toousers usando Olá portal do Azure, as ferramentas de linha de comando do Azure ou APIs de gerenciamento do Azure.

Para obter mais informações sobre aspectos básicos de RBAC do Azure, consulte [começar com controle de acesso baseado em função no hello Portal do Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>Como fazer para gerenciar o RBAC do Azure com o PowerShell?

Você pode usar os cmdlets de PowerShell toomanage RBAC do Azure, incluindo Olá tarefas de gerenciamento a seguir:

- Listar funções

- Veja quem tem acesso

- Conceder acesso

- Remover acesso

- Criar uma função personalizada

- Obter ações para um provedor de recursos

- Modificar uma função personalizada

- Excluir uma função personalizada

- Listar funções personalizadas

Para obter instruções sobre como toomanage RBAC do Azure com o PowerShell, consulte [acesso baseado em função gerenciar com o Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Autenticação Multifator do Azure

[Autenticação multifator do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) é uma solução de verificação de duas etapas que ajuda a proteger acesso toodata e aplicativos, enquanto atende a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte por meio de uma variedade de métodos de verificação, incluindo chamada telefônica, mensagem de texto ou verificação de aplicativo móvel.

toodeploy MFA Olá nuvem do Azure, você precisa toofirst habilitá-lo e, em seguida, ativar a verificação em duas etapas para os usuários.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Como habilitar o Azure toouse MFA?

Se os usuários tiverem licenças que incluem autenticação multifator do Azure, não há nada que você precisa tooturn toodo no Azure MFA. Caso contrário, você precisa toocreate um provedor de multi-Factor Auth em seu diretório. toodo isso, siga estas etapas:

1. Selecione **do Active Directory** em Olá portal clássico do Azure (conectado como administrador).

2. Selecione **Provedores de Autenticação Multifator.**

3. Selecione **Novo** e, em seguida, em **Serviços de Aplicativos**, selecione **Provedor de Autenticação Multifator.**

4. Selecione **Criação Rápida.**

5. Preencha o campo de nome hello e selecione um modelo de uso (por autenticação ou por usuário habilitado).

6. Designa um diretório ao qual Olá provedor MFA está associado.

7. Clique em Olá **criar** botão.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Para obter mais instruções sobre como toomanage seu provedor de autenticação multifator, consulte [guia de Introdução com um provedor de autenticação multifator do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>Como fazer para ativar a verificação em duas etapas para os usuários?

Você pode impor a verificação em duas etapas para todas as entradas ou você pode criar a verificação de duas etapas de toorequire de políticas de acesso condicional somente quando condições específicas.

Habilitar o Azure MFA alterando estados do usuário é a abordagem tradicional Olá para exigir a verificação em duas etapas. Todos os usuários de saudação que permitem que você terá Olá verificacao do mesmo requisito tooperform toda vez que entrar. A habilitação de um usuário substitui qualquer política de acesso condicional que possa afetar esse usuário.

A habilitação do MFA do Azure com uma política de acesso condicional é uma abordagem mais flexível para exigir a verificação em duas etapas. Você pode criar políticas de acesso condicional que se aplicam a toogroups, bem como para usuários individuais. Grupos de alto risco podem receber mais restrições do que grupos de baixo risco, ou a verificação em duas etapas pode ser exigida apenas para aplicativos de nuvem de alto risco e ignorada para os de baixo risco. No entanto, o acesso condicional um recurso pago do Azure Active Directory.

tooenable MFA por meio da alteração de estado do usuário, Olá a seguir:

1. Entre toohello portal do Azure como administrador.
2. Vá muito**Active Directory do Azure \> usuários e grupos \> todos os usuários**.
3. Selecione **Autenticação Multifator**.
4. Localizar Olá usuário que você deseja tooenable para o Azure MFA. Talvez seja necessário toochange Olá exibição na parte superior da saudação.
5. Verifique o nome da saudação caixa próxima toohello do usuário.
6. Olá à direita, em etapas rápidas, escolha **habilitar**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Confirme sua seleção na janela pop-up de saudação que é aberta.  Os usuários para quem o MFA tiver sido habilitado deverá Olá tooregister próxima vez que entrar.

tooenable MFA do Azure com uma política de acesso condicional, Olá a seguir:

1. Entre toohello portal do Azure como administrador.

2. Vá muito**Active Directory do Azure \> acesso condicional**.

3. Selecione **Nova política**.

4. Em **Atribuições**, selecione **Usuários e grupos**. Saudação de uso **incluir** e **excluir** guias toospecify quais usuários e grupos que será gerenciado pela política de saudação.

5. Em **Atribuições**, selecione **Aplicativos de nuvem.** Escolha muito**incluem todos os aplicativos de nuvem**.
6.  Em **Controles de acesso**, selecione **Grant**. Escolha **Exigir autenticação multifator**.
7.  Ativar **habilitar política** muito**na** e, em seguida, selecione **salvar**.

Para obter informações sobre como tooconfigure Azure MFA configurações tooset os alertas de fraude, criar um bypass avulso, usar mensagens de voz personalizadas, configurar o cache, especifique IPs confiáveis, criar senhas de aplicativo, habilitar a MFA para dispositivos que os usuários de confiança e selecione lembrar-se métodos de verificação, consulte [definir configurações de autenticação de multifator do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Próximas etapas

- [Protegendo o acesso privilegiado no Azure AD](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Perguntas frequentes sobre a Autenticação Multifator do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Solução de problemas do Controle de Acesso Baseado em Função](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
