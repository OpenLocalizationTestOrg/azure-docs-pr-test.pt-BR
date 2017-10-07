---
title: "usuários do Active Directory do Azure aaaLicense em Olá portal clássico do Azure | Microsoft Docs"
description: "Descrição de licenciamento do Microsoft Azure Active Directory, como ele funciona, como tooget iniciada e práticas recomendadas, inclusive o Office 365, Microsoft Intune e Azure Active Directory Premium e edições Basic"
services: active-directory
keywords: Licenciamento do AD do Azure
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>O que é Microsoft Azure Active Directory licenciamento no hello portal clássico do Azure?

> [!div class="op_single_selector"]
> * [Obter instruções do Portal do Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Informações sobre o portal clássico do Azure](active-directory-licensing-what-is.md)
>
>

O Active Directory do Azure (Azure AD) é a identidade da Microsoft como uma solução e plataforma de serviço (IDaaS). O AD do Azure é oferecido em várias versões de técnicas e funcionais desde o Azure AD gratuito, que está disponível com qualquer serviço da Microsoft, como Office 365, Dynamics, Microsoft Intune e do Azure (AD do Azure não gerar todos os encargos de consumo nesse modo), tooAzure AD paga versões, como o Enterprise Mobility Suite (EMS), Azure AD Premium e Basic, bem como do Azure multi-Factor Authentication (MFA). Como muitos serviços online da Microsoft, a maioria das versões pagas do AD do Azure é fornecida por meio de direitos de usuário, como é no Office 365, Microsoft Intune e AD do Azure. Nesses casos, compra do serviço de saudação é representada com uma ou mais assinaturas, e cada assinatura inclui um número de pré-compra de licenças em seu locatário. Direitos de usuário são obtidos por meio da atribuição de licença, criar um vínculo entre o usuário hello e produto hello, permitindo que os componentes de serviço Olá para usuário Olá, e consumindo uma saudação pago licenças.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como centralizar tooassign funções de administrador na administração de saudação do AD do Azure, consulte [de licença por conta própria e seus usuários no AD do Azure](active-directory-licensing-get-started-azure-portal.md).

[Experimente o Azure AD Premium agora.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Portal de administração do AD do Azure é uma parte da saudação portal clássico do Azure. Embora o uso do Azure AD não exija nenhuma compra do Azure, o acesso a esse portal requer uma assinatura ativa do Azure ou uma [assinatura de avaliação do Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

Para obter uma visão geral ampla dos recursos de serviço do AD do Azure, confira [O que é o AD do Azure](active-directory-whatis.md).
[Saiba mais sobre os níveis de serviço do AD do Azure](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Assinaturas do Azure pré-pago são diferentes: enquanto também são representados em seu diretório, essas assinaturas habilitar a criação de recursos do Azure e mapeá-los tooyour de pagamento. Nesse caso, há nenhum contagens de licença associadas à assinatura hello. Associação de usuários com assinatura hello, acesso toomanaging assinatura de recursos os usuários da saudação é obtida conceder permissões toooperate em recursos do Azure mapeados toohello assinatura.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Como funciona o trabalho de licenciamento do AD do Azure?
Os Serviços do AD do Azure baseados em licença (baseados em direito) funcionam ativando uma assinatura no locatário de serviço/diretório do AD do Azure. Depois de saudação assinatura está ativa recursos de serviço de saudação podem ser gerenciados por administradores de serviço de diretório/e usados por usuários licenciados.

Quando você compra ou ativar o Enterprise Mobility Suite, Azure AD Premium ou Azure AD Basic, seu diretório é atualizado com assinatura hello, incluindo o período de validade e pago licenças. As informações de assinatura, incluindo status, próximo evento de ciclo de vida e número de saudação de licenças atribuídas ou disponíveis está disponível por meio de saudação portal clássico do Azure, na guia de licenças de saudação de diretório específico do hello. Isso também é toobest local toomanage suas atribuições de licença.

Cada assinatura consiste em um ou mais planos de serviço, cada Olá mapeamento incluídos nível funcional de saudação do tipo de serviço; Por exemplo, AD do Azure, o Azure MFA, Microsoft Intune, Exchange Online ou SharePoint Online. O gerenciamento de licença do AD do Azure não requer gerenciamento de nível de plano de serviço. Isso é diferente do Office 365, que depende do modo toomanage acesso tooincluded services essa configuração avançada. O AD do Azure depende na configuração de serviço, recursos tooenable e gerenciar permissões individuais.

Em geral, informações de assinatura do AD do Azure são gerenciadas por meio de saudação portal clássico do Azure, na guia de licenças de saudação de diretório específico do hello. Assinaturas de AD do Azure, com exceção de saudação do Azure AD Premium, não aparecem no portal do Office de hello.

> [!IMPORTANT]
> Azure AD Premium e Basic, bem como as assinaturas do Enterprise Mobility Suite, são tootheir confinado provisionado/locatário do diretório. As assinaturas não podem ser divididas entre diretórios ou usuários tooentitle usada em outros diretórios. Mover uma assinatura entre diretórios é possível, mas requer a enviar um tíquete de suporte ou cancelamento e adquirir novamente em caso de saudação de compras diretos.
>
> Ao comprar o Azure AD ou Enterprise Mobility Suite por meio de licenciamento por Volume da ativação da assinatura ocorrerá automaticamente quando o contrato de saudação inclui outros serviços Online da Microsoft, por exemplo, Office 365.
>
>

Recursos do AD do Azure pagos amplitude Olá alcance do diretório de saudação. Os exemplos incluem:

* A atribuição baseada em grupo tooapplications, que é habilitado em aplicativos específicos hello, que você está gerenciando.
* Recursos de gerenciamento de grupo de autoatendimento estão disponíveis em configuração do diretório hello ou grupo específico hello e avançadas.
* Relatórios de segurança Premium estão na guia relatório de saudação
* Detecção de aplicativos de nuvem aparece na Olá portal do Azure na identidade.

### <a name="assigning-licenses"></a>Atribuindo licenças
Ao obter uma assinatura é que tudo o que você precisa tooconfigure paga recursos, usar o AD do Azure recursos pagos requer distribuindo indivíduos certos de toohello de licenças. Em geral, qualquer usuário que deve ter tooor de acesso que é gerenciado por meio do AD do Azure paga o recurso deve ser atribuído uma licença. Uma atribuição de licença é um mapeamento entre um usuário e um serviço comprado, como o AD Premium, Basic do Azure ou o Enterprise Mobility Suite.

O gerenciamento de usuários em seu diretório deve ter uma licença e é simples. Ele pode ser feito, atribuindo tooa grupo toocreate as regras de atribuição por meio do portal de administração do AD do Azure hello ou atribuir licenças diretamente a indivíduos certos toohello por meio de um portal, o PowerShell ou APIs. Ao atribuir o grupo de tooa de licenças, todos os membros do grupo receberão uma licença. Se os usuários são adicionados ou removidos do grupo de saudação serão licença adequada Olá atribuídos ou removidos. Atribuição de grupo pode utilizar qualquer tooyou disponíveis de gerenciamento de grupo e é consistente com a atribuição baseada em grupo tooapplications. Usando essa abordagem, você pode configurar regras de modo que todos os usuários em seu diretório são atribuídos automaticamente, certifique-se de que todos com cargo apropriado da saudação tem uma licença ou até mesmo delegar gerenciadores de tooother decisão Olá na organização hello.

Com a atribuição de licença baseada em grupo, qualquer usuário que tem um local de uso herdará o local do diretório de saudação durante a atribuição. Esse local pode ser alterado pelo administrador de saudação a qualquer momento. Em casos onde Olá automatizada falhou devido a atribuição tooerror, informações de usuário de saudação em que o tipo de licença refletirá o estado.

## <a name="getting-started-with-azure-ad-licensing"></a>Introdução ao licenciamento do AD do Azure
Guia de Introdução ao AD do Azure é fácil. Você sempre pode criar seu diretório como parte da assinatura de avaliação gratuita do Azure tooa. [Saiba mais sobre como se inscrever como uma organização](sign-up-organization.md). seguir Olá pode ajudá-lo a Certifique-se de que seu diretório melhor é alinhado com outros serviços da Microsoft possam consumir ou estiver planejando tooconsume e suas metas na obtenção de serviço de saudação.

Estas são algumas das práticas recomendadas:

* Se você está usando algum dos serviços organizacionais da Microsoft, já tem um diretório do Azure AD. Nesse caso, você deve continuar toouse Olá mesmo diretório para outros serviços, para que o gerenciamento de identidade de núcleo, incluindo o provisionamento e híbrida SSO, pode ser utilizado em serviços de saudação. Os usuários terão uma experiência de logon único e se beneficiarão de recursos mais avançados em serviços de saudação. Como resultado, se você decidir toobuy um AD do Azure paga service para sua força de trabalho, é recomendável que você use Olá toodo do mesmo diretório isso.
* Se você estiver planejando toouse AD do Azure para um conjunto diferente de usuários (parceiros, clientes e assim por diante), ou se você gostaria que os serviços tooevaluate AD do Azure e gostaria de toodo que em isolamento de seu serviço de produção, ou se você estiver procurando toosetup um ambiente de área restrita para os serviços, é recomendável que você primeiro crie um novo diretório por meio do portal clássico do Azure Azure hello. [Saiba mais sobre como criar um novo diretório do AD do Azure no portal clássico do Azure de saudação](active-directory-licensing-directory-independence.md). diretório de novo Olá será criado com sua conta como um usuário externo com permissões de administrador global. Quando você entrar no toohello clássico do Azure portal com esta conta, que será capaz de toosee esse diretório e acessar todas as tarefas de administração do diretório. É recomendável que você crie uma conta local com privilégios apropriados toomanage outros serviços da Microsoft (aqueles que não pode ser acessado por meio de saudação portal clássico do Azure). [Saiba mais sobre como criar contas de usuário no AD do Azure](active-directory-create-users.md).

> [!NOTE]
> O AD do Azure dá suporte a "usuários externos", que são contas de usuário em uma instância do AD do Azure, criadas usando uma MSA (Conta da Microsoft) ou uma identidade do AD do Azure de outro diretório. Enquanto estamos ocupados estender esse recurso em todos os serviços de organizacionais da Microsoft, no momento essas contas não têm suporte em algumas experiências de serviços hello; Por exemplo, o portal de administração do Office 365 de saudação não suporta atualmente esses usuários. Como resultado, usuários externos com contas da Microsoft não será capaz de tooaccess do portal de administração Olá Office 365, enquanto os usuários externos de outros diretórios do AD do Azure serão ignorados. No caso hello, conta local de único usuário hello, Olá AD do Azure ou Office 365 diretório onde o usuário Olá foi criado originalmente, poderão ser acessados por meio dessas experiências.
>
>

Como indicado, o AD do Azure tem diferentes versões pagas. Essas versões têm algumas pequenas diferenças em sua disponibilidade de compra:

| Produto | EA/VL | Aberto | CSP | Direitos de uso do MPN | Compra direta | Avaliação |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| AD Premium do Azure |X |X |X | |X |X |
| AD Basic do Azure |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Selecione uma ou mais avaliações de licença
 Em todos os casos, você pode ativar uma assinatura de avaliação do Azure AD Premium ou Enterprise Mobility Suite selecionando avaliação específico de saudação desejado na guia de licenças Olá em seu diretório. Qualquer avaliação contém uma assinatura de 30 dias com 100 licenças.

![Planos de licença de avaliação do Active Directory do Azure](./media/active-directory-licensing-what-is/trial_plans.png)

![Planos de licença de avaliação do Enterprise Mobility Suite](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Ativar planos de licença de avaliação](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Atribuir licenças
Quando Olá assinatura estiver ativa, você deve atribuir uma licença tooyourself e Olá navegador tooensure você está vendo todos os seus recursos de atualização. Olá, próxima etapa é tooassign licenças usuários toohello que precisará tooaccess ou ser incluídos em paga recursos do AD do Azure. Conforme mencionado acima em "Atribuindo licenças," hello melhor maneira toodo isso é tooidentify Olá grupo que representa o público-alvo Olá desejado e atribuí-lo a licença toohello; Dessa forma, os usuários que são adicionados ou removidos do grupo de saudação durante seu ciclo de vida serão atribuídos tooor removido da licença de saudação.

tooassign um grupo de licenças tooa ou usuários individuais, selecionados Olá plano de licença, você deseja tooassign e clique em **atribuir** na barra de comandos de saudação.

![Ativar planos de licença de avaliação](./media/active-directory-licensing-what-is/assign_licenses.png)

Depois que a caixa de diálogo Olá atribuição para o plano selecionado hello, você pode selecionar usuários e adicioná-los toohello **atribuir** coluna saudação à direita. Você pode ver a lista de saudação do usuário ou pesquisar indivíduos específicos usando Olá procurando vidro em Olá parte superior direita da grade de usuário hello. grupos de tooassign, selecione "Grupos" de saudação **Mostrar** menu e, em seguida, clique o botão de seleção de saudação nas atribuições de saudação do hello toorefresh direita que são exibidos.

![Atribuir licenças toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Agora você pode pesquisar ou página por meio de grupos e adicioná-las toohello **atribuir** coluna Olá mesma maneira. Você pode usar esses tooassign uma combinação de usuários e grupos em uma única operação. toocomplete Olá o processo de atribuição, clique botão de seleção de saudação em Olá canto inferior direito da página de saudação.

![Mensagem de progresso da atribuição de licença](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Quando um grupo é atribuído, seus membros herdam licenças hello dentro de 30 minutos, mas geralmente dentro de 1 a 2 minutos.

Erros de atribuição podem ocorrer durante a atribuição de licença do AD do Azure, mas são relativamente raros. Os possíveis erros de atribuição estão limitados a:

* Conflito de atribuição - quando um usuário foi anteriormente atribuída uma licença que é incompatível com a licença atual hello. Nesse caso, a atribuição de licença nova Olá exigirá removendo Olá anterior.
* Licenças disponíveis excedidas - quando Olá o número de usuários em grupos atribuídos excede licenças disponíveis, status de atribuição de usuários Olá refletirão tooassign uma falha devido toomissing licenças.

### <a name="view-assigned-licenses"></a>Exibir licenças atribuídas
Uma exibição resumida de licenças atribuídas, incluindo eventos de ciclo de vida de assinatura disponíveis, atribuído e Avançar são exibidos em Olá **licenças** guia.

![Exibir hello número de licenças atribuídas](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Uma lista detalhada de usuários e grupos atribuídos, incluindo status e caminho da atribuição (direta ou herdada de um ou mais grupos) estão disponíveis ao navegar em um plano de licença.

![Exibição de detalhes de licenças atribuídas a um plano de licença](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Remover licenças é tão fácil quanto atribuí-las. Se o usuário hello está diretamente atribuído ou para um grupo, você pode remover a licença Olá selecionando o tipo de licença hello, selecionando **remover**, adicionando o usuário hello ou lista do grupo toohello remover e confirmar a ação de saudação. Como alternativa, você pode abrir um tipo de licença, Olá Selecionar usuário ou grupo específico e toque em **remover** na barra de comandos de saudação. tooend herança de um usuário de uma licença de um grupo, simplesmente remover usuário de saudação do grupo de saudação.

### <a name="extending-trials"></a>Estendendo avaliações
Extensões de avaliação para clientes que estão disponíveis como Self-service portal Olá Office 365. Um administrador do cliente pode navegar toohello [portal do Office](https://portal.office.com/#Billing) (acesso depende das permissões para o portal do Office Olá) e selecione a versão de avaliação do Azure AD Premium. Clique em Olá **Estender avaliação** link e siga as instruções de saudação. Você precisará tooenter um cartão de crédito, mas ele não será cobrado.

![Estendendo uma avaliação de licença no portal do Office Olá](./media/active-directory-licensing-what-is/extend_license_trial.png)

Clientes também podem solicitar uma extensão da avaliação enviando uma solicitação de suporte. Um administrador do cliente pode navegar portal do Office 365 de toohello [página de suporte](http://aka.ms/extendAADtrial) (acesso depende das permissões para a página de suporte do Office de hello). Nesta página, selecione "Assinaturas e Avaliações" em Recursos e "Perguntas de avaliação" em Sintoma. Por fim, insira informações em circunstâncias Olá

![Estendendo uma avaliação usando uma solicitação de suporte](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Próximas etapas
Agora você pode ser tooconfigure pronto e usar alguns recursos do Azure AD Premium.

* [Redefinição de senha de autoatendimento](active-directory-manage-passwords.md)
* [Gerenciamento de grupo de autoatendimento](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Tooapplications de atribuição de grupo](active-directory-manage-groups.md)
* [Autenticação Multifator do Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Compra direta de licenças do AD Premium do Azure](http://aka.ms/buyaadp)
