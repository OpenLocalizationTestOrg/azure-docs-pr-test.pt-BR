---
title: "Proteção de identidade do Active Directory de aaaAzure | Microsoft Docs"
description: "Saiba como Azure AD Identity Protection permite que você toolimit capacidade Olá tooexploit um invasor uma identidade comprometida ou dispositivo e toosecure uma identidade ou um dispositivo que era anteriormente conhecido ou suspeita toobe comprometido."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Proteção contra identidade Active Directory do Azure é um recurso de edição de saudação do Azure AD Premium P2 que permite que você:

- Detectar possíveis vulnerabilidades que afetam as identidades da organização

- Configurar respostas automatizadas toodetected suspeitas ações de identidades da organização tooyour relacionados  

- Investigar incidentes suspeitos e tomar a ação apropriada tooresolve-los   


## <a name="getting-started"></a>Introdução

A Microsoft protege identidades baseadas em nuvem há mais de uma década. Com o Azure Active Directory Identity Protection em seu ambiente, você pode usar Olá mesmos sistemas de proteção Microsoft usa toosecure identidades.

maioria de saudação de levar violações de segurança colocar quando os invasores obterem o ambiente de tooan acesso pelo roubo de identidade do usuário. Ao longo de anos de hello, os invasores tornaram cada vez mais eficazes, aproveitando as violações de terceiros e uso de ataques de phishing sofisticados. Assim que um invasor obtiver acesso a contas de usuário com privilégios baixos tooeven, é relativamente fácil tooimportant toogain acessar recursos da empresa por meio de movimentação lateral.

Como consequência, você precisa:

- Proteger todas as identidades, independentemente do nível de privilégio

- Agir proativamente para evitar o uso de identidades comprometidas

Descobrir identidades comprometidas não é uma tarefa fácil. Active Directory do Azure usa algoritmos de aprendizado de máquina adaptável e anomalias de toodetect heurística e incidentes suspeitos que indicam potencialmente comprometidos identidades. Usando esses dados, proteção de identidade gera relatórios e alertas que permitem que você tooevaluate Olá detectou problemas e tomar ações de correção ou atenuação apropriada.

O Azure Active Directory Identity Protection é mais do que apenas uma ferramenta de monitoramento e criação de relatórios. tooprotect identidades da sua organização, você pode configurar políticas baseadas em risco que respondem automaticamente toodetected problemas quando um nível de risco especificado for atingido. Essas políticas, além de tooother condicional acessar controles fornecidos pelo Active Directory do Azure e o EMS, pode bloquear automaticamente ou iniciar ações de correção adaptável, inclusive redefinições de senha e a imposição de autenticação multifator.


#### <a name="identity-protection-capabilities"></a>Recursos do Identity Protection

**Detecção de vulnerabilidades e contas de risco:**  

* Fornecendo recomendações personalizadas tooimprove postura de segurança geral, realçando vulnerabilidades
* Calcular os níveis de risco de entrada
* Calcular os níveis de risco do usuário


**Investigação dos eventos de risco:**

* Enviar notificações para eventos de risco
* Investigar os eventos de risco usando informações relevantes e contextuais
* Fornecendo tootrack investigações de fluxos de trabalho básicos
* Fornecer acesso fácil tooremediation ações, como a redefinição de senha

**Políticas de acesso condicional baseadas em risco:**

* Diretiva toomitigate arriscadas entradas bloqueando entradas ou a necessidade de desafios de autenticação multifator.
* Diretiva tooblock ou contas de usuário de arriscados segura
* Diretiva toorequire usuários tooregister para autenticação multifator



## <a name="identity-protection-roles"></a>Funções da proteção de identidade

atividades de gerenciamento tooload saldo Olá em torno de sua implementação de proteção de identidade, você pode atribuir várias funções. O Azure AD Identity Protection dá suporte a três funções do diretório:

| Função                         | O que ele pode fazer                          | O que não pode fazer
| :--                          | ---                                |  ---   |
| Administrador global         | Acesso completo tooIdentity proteção integrada de proteção de identidade| |
| Administrador de segurança       | Acesso completo tooIdentity proteção | Proteção de Identidade integrada, redefinir senhas para um usuário |
| Leitor de segurança              | Acesso somente leitura tooIdentity proteção | Integrar Proteção de Identidade, corrigir usuários, configurar políticas, redefinir senhas |




Para saber mais detalhes, consulte [Atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Detecção

### <a name="vulnerabilities"></a>Vulnerabilidades

O Azure Active Directory Identity Protection analisa sua configuração e detecta vulnerabilidades que podem ter impacto nas identidades do usuário. Para saber mais, confira [Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Eventos de risco

Active Directory do Azure usa algoritmos e heurística toodetect suspeitas ações de identidades do usuário relacionadas tooyour de aprendizado de máquina adaptável. sistema de saudação cria um registro para cada ação suspeita detectada. Esses registros também são conhecidos como eventos de risco.  
Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).


## <a name="investigation"></a>Investigação
Sua jornada com proteção de identidade normalmente inicia com o painel de proteção de identidade hello.

![Correção](./media/active-directory-identityprotection/1000.png "Correção")

painel Olá fornece acesso para:

* Relatórios, como **Usuários sinalizados por riscos**, **Eventos de risco** e **Vulnerabilidades**
* As configurações como a configuração de saudação do seu **políticas de segurança**, **notificações** e **registro de autenticação multifator**

Normalmente é o ponto de partida para investigação, que é o processo de saudação de revisão Olá atividades, logs e outras informações relevantes tooa relacionado toodecide de evento de risco se são necessárias etapas de correção ou de redução, e como a identidade de saudação foi comprometido e entender como Olá comprometidos identidade foi usada.

É possível vincular sua toohello de atividades de investigação [notificações](active-directory-identityprotection-notifications.md) proteção do Azure Active Directory envia por email.

Olá seções a seguir fornecem mais detalhes e etapas Olá investigação tooan relacionados.  


## <a name="risky-sign-ins"></a>Entradas de risco

O Azure Active Directory detecta [tipos de evento de risco](active-directory-reporting-risk-events.md#risk-event-types) em tempo real e offline. Cada evento de risco que foi detectado para uma entrada de um usuário contribui tooa conceito lógico chamado entrar arriscado. Uma entrada arriscado é um indicador para uma tentativa de logon que não pode ter sido realizada pelo proprietário da saudação legítimo de uma conta de usuário.


### <a name="sign-in-risk-level"></a>Nível de risco de entrada

Um nível de risco de entrada é uma indicação (alto, médio ou baixo) de probabilidade Olá que uma tentativa de logon não foi executada pelo proprietário da saudação legítimo de uma conta de usuário.

### <a name="mitigating-sign-in-risk-events"></a>Mitigação de eventos de risco de entrada

Uma redução é uma ação toolimit Olá capacidade um invasor tooexploit uma identidade comprometida ou dispositivo sem estado de restauração Olá identidade ou dispositivo tooa seguro. Uma redução não resolver anterior eventos de entrada risco associados à identidade hello ou dispositivo.

toomitigate arriscados entradas automaticamente, você pode configurar o risco de entrada policicies de segurança. Usando essas diretivas, considere o nível de risco de saudação do usuário hello ou Olá entrar tooblock entradas arriscadas ou exigir autenticação multifator do hello usuário tooperform. Essas ações podem impedir que um invasor explorar um dano de toocause roubo de identidade e podem fornecer uma identidade de Olá de toosecure algum tempo.

### <a name="sign-in-risk-security-policy"></a>Política de segurança de risco de entrada
Uma política de risco de entrada é uma política de acesso condicional que é avaliada Olá risco tooa sign-in específico e aplica atenuações com base em regras e condições predefinidas.

![Política de risco de entrada](./media/active-directory-identityprotection/1014.png "Política de risco de entrada")

Azure AD Identity Protection ajuda você a gerenciar a mitigação de saudação de entradas arriscadas, permitindo que você:

* Definir Olá usuários e grupos Olá política aplica-se a:

    ![Política de risco de entrada](./media/active-directory-identityprotection/1015.png "Política de risco de entrada")
* Defina Olá entrar risco nível limite (baixa, média ou alta) que dispara a política de saudação:

    ![Política de risco de entrada](./media/active-directory-identityprotection/1016.png "Política de risco de entrada")
* Conjunto Olá controles toobe imposta quando a política de saudação dispara:  

    ![Política de risco de entrada](./media/active-directory-identityprotection/1017.png "Política de risco de entrada")
* Alternar estado Olá da política:

    ![Registro de MFA](./media/active-directory-identityprotection/403.png "Registro de MFA")
* Revisar e avaliar o impacto de saudação de uma alteração antes de ativá-lo:

    ![Política de risco de entrada](./media/active-directory-identityprotection/1018.png "Política de risco de entrada")

#### <a name="what-you-need-tooknow"></a>O que você precisa tooknow
Você pode configurar uma autenticação multifator do risco de entrada segurança política toorequire:

![Política de risco de entrada](./media/active-directory-identityprotection/1017.png "Política de risco de entrada")

No entanto, por motivos de segurança, essa configuração só funciona para usuários que já foram registrados na autenticação multifator. Se a autenticação de vários fatores de toorequire Olá condição é atendida para um usuário que ainda não foi registrado para autenticação multifator, usuário Olá será bloqueado.

Como prática recomendada, se você quiser toorequire multi-factor authentication arriscadas entradas, você deve:

1. Habilitar Olá [política de registro de autenticação multifator](#multi-factor-authentication-registration-policy) para Olá usuários afetados.
2. Exigir Olá afetados toologin de usuários em uma sessão não pode ser arriscado tooperform um registro MFA

A conclusão dessas etapas faz com que a autenticação multifator seja exigida em caso de entrada de risco.

#### <a name="best-practices"></a>Práticas recomendadas
Escolhendo um **alta** limite reduz o número de saudação de vezes que uma política é disparada e minimiza Olá impacto toousers.  

No entanto, ele exclui **baixo** e **médio** sinalizado como entradas para o risco da política de saudação, que não pode impedir que um invasor explorar uma identidade comprometida.

Quando a configuração Olá política,

* exclua os usuários que não tem / não podem ter a autenticação multifator
* Exclua os usuários em locais onde habilitando Olá política não é prático (por exemplo, nenhum toohelpdesk de acesso)
* Exclua os usuários que são provavelmente toogenerate muitos falsos positivos (desenvolvedores, analistas de segurança)
* use um limite **Alto** durante a distribuição inicial de política ou se você precisar minimizar os desafios encontrados pelos usuários finais.
* Use um limite **Baixo** se sua organização exigir uma segurança maior. Selecionar um limite **Baixo** apresenta desafios de entrada do usuário adicionais, porém representa uma segurança maior.

Olá recomendado padrão para a maioria das organizações é tooconfigure uma regra para um **médio** limite toostrike um equilíbrio entre segurança e facilidade de uso.

política de risco de entrada Hello é:

* Tráfego de navegador tooall aplicados e logons que usam autenticação moderna.
* Tooapplications não aplicada usando protocolos de segurança mais antigos, desabilitando o ponto de extremidade do WS-Trust de saudação IDP Olá federado, como o AD FS.

Olá **eventos de risco** página no console de proteção de identidade Olá lista todos os eventos:

* aos quais essa política se aplica
* Você pode examinar a atividade de saudação e determinar se a ação de saudação era apropriada ou não

Para obter uma visão geral de saudação relacionadas a experiência do usuário, consulte:

* [Recuperação de entrada arriscada](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Entrada arriscada bloqueada](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Experiências de entrada com o Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**caixa de diálogo de configuração relacionados de saudação tooopen**:

- Em Olá **Azure AD Identity Protection** folha em Olá **configurar** seção, clique em **risco política**.

    ![Política do usuário ridk](./media/active-directory-identityprotection/1014.png "Política do usuário ridk")



## <a name="users-flagged-for-risk"></a>Usuários sinalizados por risco

Todos os ativos [eventos de risco](active-directory-identity-protection-risk-events.md) que foram detectados pelo Azure Active Directory para um usuário contribuir tooa conceito lógico chamado risco do usuário. Um usuários sinalizado como de risco é um indicador de que uma conta de usuário pode ter sido comprometida.

![Usuários sinalizados por risco](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Nível de risco do usuário

Um nível de risco do usuário é uma indicação (alto, médio ou baixo) de probabilidade Olá Olá a identidade de usuário foi comprometida. Ele é calculado com base em eventos de risco do usuário Olá que estão associados com a identidade do usuário.

Olá status de um evento de risco é **Active** ou **fechado**. Somente eventos de risco **Active** contribuem cálculo do nível de risco do usuário toohello.

nível de risco do usuário Olá é calculada usando Olá entradas a seguir:

* Eventos de risco ativo afetar o usuário Olá
* Nível de risco desses eventos
* Se foram tomadas ações de correção

![Riscos de usuário](./media/active-directory-identityprotection/1031.png "Riscos de usuário")

Você pode usar o hello usuário risco níveis toocreate políticas de acesso condicional que impedir que usuários arriscados entrar, ou forçá-los toosecurely alterar sua senha.

### <a name="closing-risk-events-manually"></a>Fechar eventos de risco manualmente

Na maioria dos casos, você coloca as ações de correção, como eventos de risco fechar tooautomatically de redefinição de uma senha segura. No entanto, isso nem sempre é possível.  
Isso acontece, por exemplo, Olá, quando:

* um usuário com eventos de risco ativo foi excluído
* Uma investigação revela que um evento de risco relatado tem sido executar por usuário legítimo Olá

Como eventos de risco que são **Active** contribuem toohello cálculo de risco de usuário, você pode ter toomanually diminuir um nível de risco fechando os eventos de risco manualmente.  
Durante o curso de saudação da investigação, você pode escolher tootake, qualquer um dos status de saudação de toochange ações de um evento de risco:

![Ações](./media/active-directory-identityprotection/34.png "Ações")

* **Resolver** - se após investigar um evento de risco, você fez uma ação de correção apropriada sem proteção de identidade, e você achar que eventos de risco Olá devem ser considerado fechado, o evento de saudação marcar como resolvido. Eventos resolvidos definirá tooClosed de status do evento de risco hello e eventos de risco Olá não contribuirá toouser risco.
* **Marcar como falso positivo** - Em alguns casos, você pode investigar um evento de risco e descobrir que ele foi sinalizado incorretamente como uma situação arriscada. Você pode ajudar a reduzir o número de saudação de tais ocorrências marcando o evento de risco hello como falsos positivos. Isso ajudará a classificação de saudação tooimprove algoritmos de eventos semelhantes no futuro de saudação do aprendizado de máquina hello. status de saudação de eventos de falso positivo é muito**fechado** e eles não são mais contribuirá toouser risco.
* **Ignorar** - se você não executou a qualquer ação de correção, mas desejar Olá toobe de evento de risco removido da lista de ativos hello, você pode marcar um evento de risco ignorar e status de evento Olá será fechada. Eventos ignorados não contribuem toouser risco. Essa opção deve ser usada somente em circunstâncias incomuns.
* **Reativar** -corre o risco de eventos que foram fechados manualmente (escolhendo **resolver**, **falso positivo**, ou **ignorar**) pode ser reativado, definindo Olá status de evento novamente muito**Active**. Eventos de risco reativado contribuem cálculo do nível de risco do usuário toohello. Eventos de risco fechados por meio de correção (como redefinir uma senha de segurança) não podem ser reativados.

**caixa de diálogo de configuração relacionados de saudação tooopen**:

1. Em Olá **Azure AD Identity Protection** folha, em **investigar**, clique em **eventos de risco**.

    ![Redefinição de senha manual](./media/active-directory-identityprotection/1002.png "Redefinição de senha manual")
2. Em Olá **eventos de risco** lista, clique em um risco.

    ![Redefinição de senha manual](./media/active-directory-identityprotection/1003.png "Redefinição de senha manual")
3. Na folha de risco hello, clique em um usuário.

    ![Redefinição de senha manual](./media/active-directory-identityprotection/1004.png "Redefinição de senha manual")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Fechar manualmente todos os eventos de risco para um usuário
Em vez de fechar manualmente os eventos de risco de um usuário individualmente, proteção de identidade do Azure Active Directory também fornece um método tooclose todos os eventos para um usuário com um clique.

![Ações](./media/active-directory-identityprotection/2222.png "Ações")

Quando você clica em **descartar todos os eventos**, todos os eventos estão fechados e usuário Olá afetado não está mais em risco.

### <a name="remediating-user-risk-events"></a>Corrigir eventos de risco do usuário

Uma solução é toosecure uma ação que uma identidade ou um dispositivo que foi anteriormente suspeita ou toobe comprometido. Uma ação de correção restaura Olá identidade ou dispositivo tooa seguro estado e resolve anterior eventos de risco associados à identidade hello ou dispositivo.

eventos de risco do usuário tooremediate, você pode:

* Executar eventos de risco de usuário uma senha segura redefinição tooremediate manualmente
* Configurar um toomitigate de política de segurança do usuário risco ou corrigir eventos de risco do usuário automaticamente
* Recriar a imagem de dispositivo de saudação infectado  

#### <a name="manual-secure-password-reset"></a>Redefinição de senha de segurança manual
Uma redefinição de senha segura é uma solução eficaz para muitos eventos de risco e quando executada, automaticamente fecha esses eventos de risco e recalcula o nível de risco do usuário hello. Você pode usar o hello Identity Protection painel tooinitiate uma redefinição de senha para um usuário arriscado.

diálogo relacionadas Olá fornece tooreset de dois métodos diferentes de uma senha:

**Redefinir senha** - selecione **exigem Olá usuário tooreset sua senha** tooallow Olá recuperação do usuário tooself se Olá usuário tiver registrado para autenticação multifator. Durante a saudação do próximo logon do usuário, o usuário de saudação será toosolve necessária uma autenticação multifator com êxito o desafio e a senha de Olá toochange em seguida, forçado. Essa opção não estará disponível se a conta de usuário de saudação não estiver registrado a autenticação multifator.

**Senha temporária** - selecione **gerar uma senha temporária** tooimmediately invalidar senha existente hello e criar uma nova senha temporária para o usuário hello. Envie Olá nova senha temporária tooan endereço de email alternativo para o usuário hello ou o gerente do usuário toohello. Como senha Olá é temporária, usuário Olá será senha de saudação toochange solicitada ao entrar.

![Política](./media/active-directory-identityprotection/1005.png "Política")

**caixa de diálogo de configuração relacionados de saudação tooopen**:

1. Em Olá **Azure AD Identity Protection** folha, clique em **usuários sinalizados riscos**.

    ![Redefinição de senha manual](./media/active-directory-identityprotection/1006.png "Redefinição de senha manual")
2. Na lista de saudação de usuários, selecione um usuário com eventos de pelo menos um risco.

    ![Redefinição de senha manual](./media/active-directory-identityprotection/1007.png "Redefinição de senha manual")
3. Na folha de usuário hello, clique em **Redefinir senha**.

    ![Redefinição de senha manual](./media/active-directory-identityprotection/1008.png "Redefinição de senha manual")

### <a name="user-risk-security-policy"></a>Política de segurança de risco do usuário
Uma política de segurança do usuário risco é uma política de acesso condicional que avalia um usuário específico do nível tooa Olá risco e aplica as ações de correção e atenuação com base em regras e condições predefinidas.

![Política do usuário ridk](./media/active-directory-identityprotection/1009.png "Política do usuário ridk")

O Azure AD Identity Protection ajuda você a gerenciar a atenuação hello e correção de usuários sinalizados riscos, permitindo que você:

* Definir Olá usuários e grupos Olá política aplica-se a:

    ![Política do usuário ridk](./media/active-directory-identityprotection/1010.png "Política do usuário ridk")
* Defina Olá usuário risco nível limite (baixa, média ou alta) que dispara a política de saudação:

    ![Política do usuário ridk](./media/active-directory-identityprotection/1011.png "Política do usuário ridk")
* Conjunto Olá controles toobe imposta quando a política de saudação dispara:

    ![Política do usuário ridk](./media/active-directory-identityprotection/1012.png "Política do usuário ridk")
* Alternar estado Olá da política:

    ![Política do usuário ridk](./media/active-directory-identityprotection/403.png "Registro de MFA")
* Revisar e avaliar o impacto de saudação de uma alteração antes de ativá-lo:

    ![Política do usuário ridk](./media/active-directory-identityprotection/1013.png "Política do usuário ridk")

Escolhendo um **alta** limite reduz o número de saudação de vezes que uma política é disparada e minimiza Olá impacto toousers.
No entanto, ele exclui **baixo** e **médio** usuários sinalizados riscos da política de saudação, que pode não proteger identidades ou dispositivos que foram anteriormente suspeita ou toobe comprometida.

Quando a configuração Olá política,

* Exclua os usuários que são provavelmente toogenerate muitos falsos positivos (desenvolvedores, analistas de segurança)
* Exclua os usuários em locais onde habilitando Olá política não é prático (por exemplo, nenhum toohelpdesk de acesso)
* use um limite **Alto** durante a distribuição inicial de política ou se você precisar minimizar os desafios encontrados pelos usuários finais.
* use um limite **Baixo** se sua organização exigir uma segurança maior. Selecionar um limite **Baixo** apresenta desafios de entrada do usuário adicionais, porém representa uma segurança maior.

Olá recomendado padrão para a maioria das organizações é tooconfigure uma regra para um **médio** limite toostrike um equilíbrio entre segurança e facilidade de uso.

Para obter uma visão geral de saudação relacionadas a experiência do usuário, consulte:

* [Fluxo de recuperação de conta comprometida](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Fluxo de conta comprometida bloqueada](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**caixa de diálogo de configuração relacionados de saudação tooopen**:

- Em Olá **Azure AD Identity Protection** folha em Olá **configurar** seção, clique em **política de risco do usuário**.

    ![Política do usuário ridk](./media/active-directory-identityprotection/1009.png "Política do usuário ridk")

### <a name="mitigating-user-risk-events"></a>Mitigar eventos de risco do usuário
Os administradores podem definir um usuário risco política tooblock os usuários de segurança após entrar dependendo do nível de risco de saudação.

Bloquear a entrada:

* Evita a geração de saudação de novos eventos de risco de usuário para usuário Olá afetado
* Permite que os administradores toomanually corrigir eventos de risco Olá que afetam a identidade do usuário hello e restaure-o estado seguro tooa



## <a name="multi-factor-authentication-registration-policy"></a>Política de registro de autenticação multifator
Autenticação multifator do Azure é um método de verificação que você está que requer uso de saudação de mais do que apenas um nome de usuário e senha. Ele fornece uma segunda camada de segurança toouser entradas e transações.  
Recomendamos exigir a autenticação multifator do Azure para entradas de usuário porque:

* fornece autenticação forte com uma variedade de opções de verificação fácil
* Desempenha um papel fundamental na preparação de sua organização tooprotect e recuperar o comprometimento de conta

![Política do usuário ridk](./media/active-directory-identityprotection/1019.png "Política do usuário ridk")

Para obter mais detalhes, veja [O que é a Autenticação Multifator do Azure?](../multi-factor-authentication/multi-factor-authentication.md)

O Azure AD Identity Protection ajuda você a gerenciar Olá roll-out de um registro de autenticação multifator, configurando uma política que permite que você:

* Definir Olá usuários e grupos Olá política aplica-se a:

    ![Política de MFA](./media/active-directory-identityprotection/1020.png "Política de MFA")
* Conjunto Olá controles toobe imposta quando a política de saudação dispara::  

    ![Política de MFA](./media/active-directory-identityprotection/1021.png "Política de MFA")
* Alternar estado Olá da política:

    ![Política de MFA](./media/active-directory-identityprotection/403.png "Política de MFA")
* Exibir o status de registro atual hello:

    ![Política de MFA](./media/active-directory-identityprotection/1022.png "Política de MFA")

Para obter uma visão geral de saudação relacionadas a experiência do usuário, consulte:

* [Fluxo do registro de autenticação multifator](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Experiências de entrada com o Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**caixa de diálogo de configuração relacionados de saudação tooopen**:

- Em Olá **Azure AD Identity Protection** folha em Olá **configurar** seção, clique em **registro de autenticação multifator**.

    ![Política de MFA](./media/active-directory-identityprotection/1019.png "Política de MFA")

## <a name="next-steps"></a>Próximas etapas
* [Canal 9: Azure AD e Identity Show: visualização do Identity Protection](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Habilitando o Azure Active Directory Identity Protection](active-directory-identityprotection-enable.md)

* [Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md)

* [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md)

* [Notificações do Azure Active Directory Identity Protection](active-directory-identityprotection-notifications.md)

* [Guia estratégico do Azure Active Directory Identity Protection](active-directory-identityprotection-playbook.md)

* [Glossário do Azure Active Directory Identity Protection.](active-directory-identityprotection-glossary.md)

* [Experiências de entrada com o Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Proteção do Azure Active Directory identidade - como toounblock usuários](active-directory-identityprotection-unblock-howto.md)

* [Introdução ao Azure Active Directory Identity Protection e ao Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
