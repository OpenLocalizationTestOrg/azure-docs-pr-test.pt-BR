---
title: "aaaWhat é a inscrição de autoatendimento do Azure? | Microsoft Docs"
description: "Uma inscrição de autoatendimento de visão geral do Azure, como toomanage Olá o processo de inscrição e tootake sobre um nome de domínio DNS."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>O que é a inscrição no Azure por autoatendimento?
Este tópico explica o processo de inscrição de autoatendimento hello e como tootake sobre um nome de domínio DNS.  

## <a name="why-use-self-service-signup"></a>Por que usar a inscrição por autoatendimento?
* Get tooservices de clientes que desejam mais rapidamente.
* Crie ofertas baseadas em email para um serviço.
* Crie fluxos de inscrição com base no email que permitem aos usuários rapidamente a identidades de toocreate usando seus aliases de email de trabalho fácil de lembrar.
* Diretórios do Azure não gerenciados podem ser feitos em diretórios gerenciados posteriormente e reutilizados para outros serviços.

## <a name="terms-and-definitions"></a>Termos e definições
* **Assinatura de autoatendimento**: Este é o método hello pelo qual um usuário se inscreve para um serviço de nuvem e tem uma identidade automaticamente criada para eles no Azure Active Directory (AD do Azure) com base em seu domínio de email.
* **Diretório do Azure não gerenciado**: Este é o diretório Olá onde essa identidade é criada. Um diretório não gerenciado é um diretório sem nenhum administrador global.
* **Usuário verificado por email**: Este é um tipo de conta de usuário no AD do Azure. Um usuário que tem uma identidade criada automaticamente após a inscrição para uma oferta de autoatendimento é conhecido como um usuário verificado por email. Um usuário verificadas por email é um membro comum de um diretório marcado com creationmethod=EmailVerified.

## <a name="user-experience"></a>Experiência do usuário
Por exemplo, digamos que um usuário cujo email é Dan@BellowsCollege.com recebe arquivos confidenciais por email. Olá arquivos foram protegidos pelo Azure Rights Management (Azure RMS). Mas a organização de Dan, a faculdade Bellows, não se inscreveu para o Azure RMS, nem implantou o RMS do Active Directory. Nesse caso, Dan pode se inscrever para uma assinatura gratuita tooRMS para pessoas físicas em arquivos de saudação protegido tooread ordem.

Se Dan for o primeiro usuário Olá com um endereço de email de toosign BellowsCollege.com para essa oferta de autoatendimento, em seguida, um não gerenciado diretório será criado para BellowsCollege.com no AD do Azure. Se outros usuários do domínio de BellowsCollege.com Olá inscrevem-se para essa oferta ou uma oferta semelhante de autoatendimento, também terão contas de usuário verificadas email criadas no hello mesmo não gerenciado diretório no Azure.

## <a name="admin-experience"></a>Experiência de admin
Um administrador que possui o nome de domínio DNS Olá de um diretório do Azure não gerenciado pode assumir ou mesclar directory Olá depois comprova a propriedade. Olá próximas seções explicam a experiência de administração hello mais detalhadamente, mas aqui está um resumo:

* Quando você faz em um diretório do Azure não gerenciado, você simplesmente se tornar administrador global de saudação do diretório não gerenciado hello. Isso às vezes é chamado de uma tomada de controle interna.
* Quando você mesclar um diretório do Azure não gerenciado, você adicionar nome de domínio DNS Olá de saudação não gerenciado tooyour gerenciado do Azure diretório e um mapeamento de usuários de recursos é criado para os usuários podem continuar tooaccess serviços sem interrupções. Isso às vezes é chamado de uma tomada de controle externa.

## <a name="what-gets-created-in-azure-active-directory"></a>O que é criado no Active Directory do Azure?
#### <a name="directory"></a>diretório
* Um diretório do Active Directory do Azure para o domínio de saudação é criado, um diretório por domínio.
* diretório do AD do Azure Olá não tem nenhum administrador global.

#### <a name="users"></a>Usuários
* Para cada usuário que se inscreve um objeto de usuário é criado no diretório do AD do Azure hello.
* Cada objeto de usuário é marcado como externo.
* Cada usuário tem o serviço toohello de acesso que eles se inscreveu.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>Como reivindico um diretório por autoatendimento do Azure AD para um domínio que possuo?
Você pode reivindicar um diretório de autoatendimento do Azure AD executando a validação de domínio. Validação de domínio prova domínio próprio hello criando registros de DNS.

Há duas maneiras toodo um controle DNS de um diretório do AD do Azure:

* controle interno (Admin descobre um diretório do Azure não gerenciado e quer tooturn em um diretório gerenciado)
* controle externo (administrador tenta tooadd um novo domínio tootheir gerenciado diretório do Azure)

Você pode estar interessado na validação de que você possui um domínio, porque você está aproveitando em um diretório não gerenciado depois que um usuário realizou a inscrição de autoatendimento, ou você pode adicionar um novo domínio tooan gerenciado diretório existente. Por exemplo, você tem um domínio nomeado contoso.com e você deseja tooadd um novo domínio chamado contoso.co.uk ou contoso.uk.

## <a name="what-is-domain-takeover"></a>O que é a tomada de controle de domínio?
Esta seção aborda como toovalidate que você possui um domínio

### <a name="what-is-domain-validation-and-why-is-it-used"></a>O que é validação de domínio e por que ela é usada?
Em operações de tooperform de pedido em um diretório, AD do Azure requer que você valide a propriedade de domínio do DNS hello.  A validação do domínio de saudação permite directory Olá tooclaim e a promover Olá autoatendimento tooa gerenciado diretório ou diretório de autoatendimento Olá mesclagem em uma existente gerenciados diretório.

## <a name="examples-of-domain-validation"></a>Exemplos de validação de domínio
Há toodo de duas maneiras de um controle DNS de um diretório:

* controle interno (por exemplo, um administrador descobre um diretório de autoatendimento, não gerenciado e quer tooturn no diretório gerenciado)
* controle externo (por exemplo, um administrador tenta tooadd um novo diretório de domínio tooa gerenciado)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>Controle interno - promover toobe um diretório de autoatendimento e não gerenciados, um diretório gerenciado
Quando você faz o controle interno, diretório Olá é convertido de um diretório de gerenciado tooa diretório não gerenciado. Você precisa de validação para nome de domínio do DNS toocomplete, onde você pode criar um registro MX ou um registro TXT na zona DNS de saudação. Essa ação:

* Valida que você possui o domínio Olá
* Torna o diretório Olá gerenciado
* Torna Olá administrador global do diretório Olá

Digamos que um administrador de TI de faculdade fole descobre que os usuários da escola Olá inscreveram para ofertas de autoatendimento. Olá registrados BellowsCollege.com nome do proprietário da saudação DNS, Olá administrador de TI pode validar a propriedade de nome DNS Olá no Azure e, em seguida, assumem o diretório não gerenciado hello. Olá directory torna-se um diretório gerenciado e Olá administrador de TI função é atribuída Olá administrador global para o diretório de BellowsCollege.com hello.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>Tomada de Controle Externa - mesclar um diretório por autoatendimento com um diretório gerenciado existente
Em um controle externo, você já tem um diretório gerenciado e desejar que todos os usuários e grupos de toojoin um diretório não gerenciado que gerenciados diretório, em vez de dois próprios separam os diretórios.

Como um administrador de um diretório gerenciado, para adicionar um domínio e domínio acontece toohave um diretório não gerenciado associado a ele.

Por exemplo, digamos que você é um administrador de TI e você já tem um diretório gerenciado para Contoso.com, um nome de domínio é registrado tooyour organização. Você descobre que os usuários de sua organização fizeram uma inscrição de autoatendimento para uma oferta usando o nome de domínio de email user@contoso.co.uk, que é outro nome de domínio possuído por sua organização. Atualmente, esses usuários têm contas em um diretório não gerenciado para contoso.co.uk.

Você não quer toomanage dois diretórios separados, para mesclar o diretório não gerenciado de saudação para contoso.co.uk em seu diretório gerenciado por TI existente para contoso.com.

Segue tomada externo Olá mesmo processo de validação de DNS que controle interno.  Diferença sendo: usuários e serviços são remapeado toohello IT diretório gerenciado.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>Qual é o impacto de saudação da execução de um controle externo?
Com um controle externo, um mapeamento de usuários de recursos é criado para que os usuários podem continuar tooaccess serviços sem interrupções. Muitos aplicativos, incluindo o RMS para indivíduos, lidar com mapeamento de saudação de recursos de usuários bem, e os usuários podem continuar tooaccess esses serviços sem alteração. Se um aplicativo não lidar com mapeamento de saudação de recursos de usuários com eficiência, controle externo pode ser bloqueado explicitamente tooprevent usuários uma experiência ruim.

#### <a name="directory-takeover-support-by-service"></a>suporte a tomada de controle do diretório pelo serviço
Olá, atualmente, controle de suporte de serviços a seguir:

* RMS

Olá serviços a seguir em breve suporte ao controle:

* PowerBI

a seguir Olá não e exige que os dados de usuário do administrador adicional ação toomigrate após um controle externo.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>Como nome do controle tooperform um domínio DNS
Você tem algumas opções para como tooperform uma validação de domínio (e fazer um controle se desejar):

1. Portal de Gerenciamento do Azure

   Uma tomada de controle é disparada por uma adição de domínio.  Se já existe um diretório para o domínio hello, você terá Olá opção tooperform um controle externo.

   Entrar toohello portal do Azure usando suas credenciais.  Navegue diretório existente tooyour e, em seguida, muito**Adicionar domínio**.
2. Office 365

   Você pode usar opções Olá Olá [gerenciar domínios](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) página no Office 365 toowork com seus domínios e registros de DNS. Consulte [Verificar seu domínio no Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).
3. Windows PowerShell

   Olá etapas a seguir é necessária tooperform uma validação usando o Windows PowerShell.

   | Etapa | Cmdlet toouse |
   | --- | --- |
   | Criar um objeto de credencial |Get-Credential |
   | Conecte-se tooAzure AD |Connect-MsolService |
   | obter uma lista de domínios |Get-MsolDomain |
   | Criar um desafio |Get-MsolDomainVerificationDns |
   | Criar registro de DNS |Fazer isso em seu servidor DNS |
   | Verificar o desafio de saudação |Confirm-MsolEmailVerifiedDomain |

Por exemplo:

1. Conecte-se tooAzure AD usando credenciais de saudação que foram usados toorespond toohello autoatendimento oferta:

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. Obter uma lista de domínios:

    Get-MsolDomain
3. Em seguida, execute toocreate de cmdlet Get-MsolDomainVerificationDns Olá um desafio:

    Get-MsolDomainVerificationDns –DomainName *seu_nome_domínio* –Mode DnsTxtRecord

    Por exemplo:

    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
4. Copie o valor de saudação (desafio Olá) que é retornado deste comando.

    Por exemplo:

    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
5. No seu namespace DNS público, crie um registro DNS txt que contém o valor Olá que você copiou na etapa anterior hello.

    Olá nome deste registro é Olá nome do domínio pai de saudação, portanto, se você criar este registro de recurso usando a função do DNS de saudação do Windows Server, deixe nome do registro Olá em branco e apenas cole o valor Olá na caixa de texto de saudação
6. Execute o desafio de Olá Olá Confirm-MsolDomain cmdlet tooverify:

    Confirm-MsolEmailVerifiedDomain -DomainName *seu_nome_domínio*

    Por exemplo:

    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com

Um desafio bem-sucedida retorna toohello prompt sem erros.

## <a name="how-do-i-control-self-service-settings"></a>Como controlar as configurações de autoatendimento?
Os administradores têm dois controles de autoatendimento atualmente. Eles podem controlar:

* Ou não os usuários podem ingressar no diretório de saudação via email.
* Se os usuários podem ou não licenciar a eles próprios para aplicativos e serviços.

### <a name="how-can-i-control-these-capabilities"></a>Como posso controlar esses recursos?
Um administrador pode configurar esses recursos usando esses parâmetros do cmdlet Set-MsolCompanySettings do AD do Azure:

* **AllowEmailVerifiedUsers** controla se um usuário pode criar ou ingressar em um diretório não gerenciado. Se você definir esse parâmetro muito$ false, não verificado de email aos usuários podem ingressar no diretório de saudação.
* **AllowAdHocSubscriptions** controla a capacidade de saudação para usuários tooperform autoatendimento inscrever-se. Se você definir esse parâmetro muito$ false, nenhum usuário pode executar inscrição de autoatendimento.

### <a name="how-do-hello-controls-work-together"></a>Como os controles de saudação funcionam em conjunto?
Esses dois parâmetros podem ser usados em conjunto toodefine controle mais preciso sobre o autoatendimento para se inscrever. Por exemplo, Olá comando a seguir permitirá que os usuários tooperform assinatura de autoatendimento, mas apenas se os usuários já tiverem uma conta no AD do Azure (em outras palavras, os usuários que seriam necessário um toobe verificar email conta criada não é possível executar assinatura de autoatendimento para cima):

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

Olá fluxograma a seguir explica todas as combinações diferentes de saudação para esses parâmetros e condições de saudação resultante para o diretório de saudação e assinatura de autoatendimento.

![][1]

Para obter mais informações e exemplos de como toouse esses parâmetros, consulte [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).

## <a name="see-also"></a>Consulte também
* [Como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)
* [PowerShell do Azure](/powershell/azure/overview)
* [Referência de Cmdlets do Azure](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
