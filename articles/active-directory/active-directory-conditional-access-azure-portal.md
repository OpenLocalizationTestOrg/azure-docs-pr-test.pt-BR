---
title: aaaAzure do Active Directory de acesso condicional | Microsoft Docs
description: "Use controle de acesso condicional no Active Directory do Azure toocheck para condições específicas ao autenticar para tooapplications de acesso."
services: active-directory
keywords: "tooapps de acesso condicional, o acesso condicional com o AD do Azure, proteger o acesso toocompany recursos, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Acesso condicional no Azure Active Directory

Em um mundo móveis, primeiro, a nuvem, o Active Directory do Azure permite toodevices de logon único, os aplicativos e serviços de qualquer lugar. Com a proliferação de saudação de dispositivos (incluindo BYOD), trabalham fora de redes corporativas e 3ª parte aplicativos de SaaS, os profissionais de TI enfrentam dois objetivos opostos:

- Capacitar Olá os usuários finais toobe produtivo sempre e
- Proteger os ativos corporativos Olá a qualquer momento

produtividade tooimprove, Active Directory do Azure fornece aos usuários com uma ampla gama de opções tooaccess seus recursos corporativos. Com o gerenciamento de acesso do aplicativo, o Active Directory do Azure permite tooensure que somente *Olá pessoas certas* pode acessar seus aplicativos. Se você desejar toohave mais controle sobre como pessoas certas Olá estão acessando os recursos sob determinadas condições? Se você ainda tiver condições sob as quais você deseja tooblock acesso toocertain aplicativos mesmo para Olá *pessoas*? Por exemplo, ele pode ser Okey para você se pessoas certas Olá acessam determinados aplicativos em uma rede confiável; No entanto, não convém-los tooaccess esses aplicativos a partir de uma rede que você não confia. Você pode tratar essas questões usando o acesso condicional.

Acesso condicional é um recurso do Active Directory do Azure que permite que você tooenforce controles Olá acesso tooapps em seu ambiente com base em condições específicas. Com controles, você pode unir ou acesso de toohello requisitos adicionais ou você pode bloqueá-lo. implementação de saudação do acesso condicional é baseada em políticas. Uma abordagem baseada em política simplifica a experiência de configuração porque ele segue maneira Olá que você pensar sobre os requisitos de acesso.  

Normalmente, você pode definir os requisitos de acesso usando as instruções que se baseiam no saudação padrão a seguir:

![Controle](./media/active-directory-conditional-access-azure-portal/10.png)

Quando você substitui duas ocorrências de saudação do "*isso*" com informações do mundo real, você tem um exemplo de uma instrução de política que parece ser familiar tooyou:

*Quando prestadores de serviço estão tentando tooaccess nossos aplicativos de nuvem de redes que não são confiáveis, bloquear o acesso.*

acima da declaração de política de saudação realça power Olá de acesso condicional. Embora você pode habilitar toobasically prestadores de serviço acessar seus aplicativos de nuvem (**que**), com acesso condicional, você também pode definir condições sob as quais Olá acesso é possível (**como**).

No contexto de saudação do acesso condicional do Active Directory do Azure,

- "**Quando isso acontecer**" chama-se **instrução de condição**
- "**, faça isso**" chama-se **controles**

![Controle](./media/active-directory-conditional-access-azure-portal/11.png)

combinação de saudação de uma instrução de condição com os controles representa uma política de acesso condicional.

![Controle](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Controles

Em uma política de acesso condicional, os controles definem o que é que deverá acontecer quando uma instrução de condição tiver sido atendida.  
Com controles, você pode bloquear o acesso ou permitir acesso com requisitos adicionais.
Quando você configura uma política que permite o acesso, você precisa tooselect no mínimo um requisito.   

### <a name="grant-controls"></a>Controles de concessão
implementação atual de saudação do Active Directory do Azure permite que você tooconfigure Olá conceder controle requisitos a seguir:

![Controle](./media/active-directory-conditional-access-azure-portal/05.png)

- **Autenticação Multifator** - você pode exigir autenticação forte por meio da autenticação multifator. Como o provedor, você pode usar a Autenticação Multifator do Azure ou um provedor de autenticação multifator local, combinados com os serviços de Federação do Active Directory (AD FS). Usando a autenticação multifator ajuda a proteger os recursos que está sendo acessado por um usuário não autorizado pode ter obtido acesso toohello credenciais de um usuário válido.

- **Dispositivo compatível** -você pode definir políticas de acesso condicional no nível do dispositivo de saudação. Você pode configurar uma diretiva tooonly ativar computadores que são compatíveis, ou os dispositivos móveis que são registrados em um tooaccess de gerenciamento de dispositivos móveis da sua organização. Por exemplo, você pode usar conformidade do dispositivo do Intune toocheck e, em seguida, relatá-lo tooAzure AD para a imposição quando o usuário Olá tentativas tooaccess um aplicativo. Para obter orientações detalhadas sobre como toouse Intune tooprotect aplicativos e dados, consulte [proteger aplicativos e dados com o Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). Você também pode usar proteção de dados de tooenforce do Intune para dispositivos perdidos ou roubados. Para saber mais, confira [Ajudar a proteger seus dados com apagamento completo ou seletivo usando o Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **Dispositivo ingressado no domínio** – você pode exigir o dispositivo Olá você usou tooconnect tooAzure do Active Directory toobe domínio tooyour do Active Directory (AD) local. Essa política se aplica a tooWindows desktops, laptops e tablets de empresa. 

Se você tiver vários controles selecionados, também será possível configurar se todos eles serão obrigatórios quando sua política for processada.

![Controle](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Controles de sessão
Controles de sessão permitem a limitação da experiência dentro de um aplicativo na nuvem. controles de sessão Olá são impostos por aplicativos de nuvem e contam com informações adicionais fornecidas pelo aplicativo do AD do Azure toohello sobre sessão de saudação.

![Controle](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Usar restrições de aplicativo impostas
Você pode usar esse controle toorequire AD do Azure toopass Olá dispositivo informações toohello nuvem aplicativo. Isso ajuda a aplicativos de nuvem Olá saber se o usuário Olá é proveniente de um dispositivo compatível ou o dispositivo ingressado no domínio. Este controle está atualmente só tem suporte com o SharePoint como aplicativo de nuvem hello. O SharePoint usa Olá dispositivo informações tooprovide os usuários uma experiência limitada ou total dependendo do estado do dispositivo hello.
Vá toolearn mais informações sobre como o acesso ao SharePoint, de limitado toorequire [aqui](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Instrução de condição

seção anterior Olá introduziu toosupported opções tooblock ou restringir o acesso tooyour recursos na forma de controles. Em uma política de acesso condicional, você definir critérios de saudação que precisa toobe atendido para sua toobe controles aplicado na forma de uma instrução de condição.  

Você pode incluir Olá atribuições a seguir em sua instrução de condição:

![Controle](./media/active-directory-conditional-access-azure-portal/07.png)


- **Quem** -em muitos casos, você deseja que seu conjunto controles toobe aplicada tooa específico de usuários. Em uma instrução de condição, você pode definir esse conjunto de selecionando usuários hello e grupos que a política se aplica. Se necessário, você pode excluir explicitamente um conjunto de usuários de sua política ao dispensá-los.  
Selecionando usuários e grupos, definir escopo de saudação de usuários que a política se aplica.    

    ![Controle](./media/active-directory-conditional-access-azure-portal/08.png)



- **O que** - normalmente, há certos aplicativos executados em seu ambiente que exigem, de uma perspectiva de proteção, mais atenção do que outros. Isso afeta, por exemplo, os aplicativos que têm acesso toosensitive dados.
Selecionando aplicativos de nuvem, definir escopo de saudação de sua política aplica-se a aplicativos na nuvem. Se necessário, você pode excluir explicitamente um conjunto de aplicativos de sua política.

    ![Controle](./media/active-directory-conditional-access-azure-portal/09.png)


- **Como** - como aplicativos de tooyour de acesso é executada sob condições que você pode controlar, há pode ser não é necessário para impor controles adicionais em como seus aplicativos de nuvem são acessados pelos usuários. No entanto, as coisas podem ser diferentes se a aplicativos de nuvem tooyour acesso é executada, por exemplo, de redes que não são confiáveis ou dispositivos que não são compatíveis. Em uma instrução de condição, você pode definir certas condições de acesso que têm requisitos adicionais, como aplicativos de tooyour de acesso é realizada.

    ![Condições](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Condições

Na implementação atual de saudação do Active Directory do Azure, você pode definir condições para Olá áreas a seguir:

- Risco de entrada
- Plataformas de dispositivo
- Locais
- Aplicativos cliente

![Condições](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Risco de entrada

Um risco de entrada é um objeto que é usado pela probabilidade de saudação do Active Directory do Azure tootrack que uma tentativa de logon não foi executada pelo proprietário da saudação legítimo de uma conta de usuário. No objeto, a probabilidade de saudação (alto, médio ou baixo) é armazenada de forma de um atributo chamado [nível de risco de entrada](active-directory-reporting-risk-events.md#risk-level). Esse objeto será gerado durante uma conexão de um usuário riscos de conexão tiverem sido detectados pelo Azure Active Directory. Para obter mais detalhes, veja [Entradas arriscadas](active-directory-identityprotection.md#risky-sign-ins).  
Você pode usar o nível de risco de entrada hello calculado como condição em uma política de acesso condicional. 

![Condições](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Plataformas de dispositivo

plataforma de dispositivo de saudação é caracterizado por sistema operacional Olá que está em execução no seu dispositivo:

- Android
- iOS
- Windows Phone
- Windows
- macOS (versão prévia). 

![Condições](./media/active-directory-conditional-access-azure-portal/02.png)

Você pode definir as plataformas de dispositivo de saudação incluídos, bem como as plataformas de dispositivo que são isentos de uma política.  
plataformas de dispositivo toouse na política hello, primeiro Olá de alteração configurar alterna muito**Sim**e, em seguida, selecione todos ou dispositivos individuais plataformas Olá política se aplica. Se você selecionar as plataformas de dispositivos individuais, política de saudação tem apenas um impacto nessas plataformas. Nesse caso, plataformas de tooother suporte para entradas não são afetadas pela política de saudação.


### <a name="locations"></a>Locais

Olá local é identificado pelo endereço IP de saudação do cliente Olá você usou tooconnect tooAzure do Active Directory. Essa condição requer toobe familiarizado com **chamado locais** e **IPs confiáveis de MFA**.  

**Chamado locais** é um recurso do Active Directory do Azure que permite que os intervalos de endereços IP toolabel confiável em sua organização. Em seu ambiente, você pode usar locais nomeadas no contexto de saudação da detecção de saudação do [eventos de risco](active-directory-reporting-risk-events.md) , bem como acesso condicional. Para obter mais detalhes sobre a configuração dos locais nomeados no Azure Active Directory, veja [locais nomeados no Azure Active Directory](active-directory-named-locations.md).

número de saudação de locais, que você pode configurar é restrito pelo tamanho de saudação do objeto relacionado Olá no AD do Azure. Você pode configurar:
 
 - Um local nomeado com backup too500 intervalos IP
 - Um máximo de 60 locais nomeadas (visualização) com um intervalo IP atribuída tooeach deles 


**IPs confiáveis de MFA** é um recurso de autenticação multifator que permite intervalos de endereços IP toodefine confiável que representa a intranet local da sua organização. Quando você configura um condições local, IPs confiáveis permite que você toodistinguish entre conexões feitas a partir da rede da sua organização e todos os outros locais. Para obter mais detalhes, veja [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



Você pode incluir todos os locais ou todos os IPs confiáveis e pode excluir todos os IPs confiáveis.

![Condições](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>Aplicativo cliente

Olá aplicativo de cliente pode ser em um aplicativo hello nível genérico (navegador da web, aplicativo móvel, cliente de desktop) você usou tooconnect tooAzure do Active Directory ou você pode selecionar especificamente o Exchange Active Sync.  
Autenticação legado refere-se tooclients usando a autenticação básica, como os clientes Office mais antigos que não usam autenticação moderna. No momento, o acesso condicional não tem suporte na autenticação herdada.

![Condições](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Cenários comuns

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exibir a autenticação multifator para aplicativos

Muitos ambientes têm aplicativos que exigem um nível mais alto de proteção que Olá outras pessoas.
Isso acontece, por exemplo, Olá para aplicativos que têm acesso toosensitive dados.
Se você quiser tooadd outra camada de proteção toothese aplicativos, você pode configurar uma política de acesso condicional que requer autenticação multifator quando os usuários acessam esses aplicativos.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exigir autenticação multifator para acesso de redes que não são confiáveis

Esse cenário é semelhante cenário anterior de toohello porque ele adiciona um requisito para autenticação multifator.
No entanto, Olá principal diferença é a condição Olá para este requisito.  
Enquanto o foco de saudação do cenário anterior Olá estava em aplicativos com dados do access toosensitve, Olá foco deste cenário é locais confiáveis.  
Em outras palavras, você pode ter um requisito para autenticação multifator se um aplicativo for acessado por um usuário de uma rede em que você não confia.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Somente os dispositivos confiáveis podem acessar os serviços do Office 365

Se você estiver usando o Intune em seu ambiente, você pode começar imediatamente usando a interface de política de acesso condicional Olá na Olá console do Azure.

Muitos clientes do Intune estão usando tooensure de acesso condicional que somente dispositivos confiáveis podem acessar os serviços do Office 365. Isso significa que os dispositivos móveis registrados com o Intune e atender aos requisitos da política de conformidade e PCs com Windows são tooan ingressado no domínio de local. Das principais melhorias é que você não tem tooset hello mesma política para cada um dos serviços de saudação Office 365.  Quando você cria uma nova política, configure Olá nuvem aplicativos tooinclude cada de saudação O365 aplicativos que você deseja tooprotect com acesso condicional.

## <a name="next-steps"></a>Próximas etapas

Se você quiser tooknow como tooconfigure uma política de acesso condicional, consulte [Introdução ao acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal-get-started.md).

Se você estiver pronto tooconfigure políticas de acesso condicional para o seu ambiente, consulte Olá [as práticas recomendadas para acesso condicional no Active Directory do Azure](active-directory-conditional-access-best-practices.md). 
