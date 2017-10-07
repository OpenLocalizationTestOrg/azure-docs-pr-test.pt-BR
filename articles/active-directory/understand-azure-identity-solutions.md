---
title: aaaUnderstand identidade do Azure | Microsoft Docs
description: "Obter um entendimento básico de recomendações para você toomake Olá melhor identidade governança decisão para sua organização, conceitos e termos de solução de identidade do Microsoft Azure."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Compreender as soluções de identidade do Azure
O Microsoft Azure Active Directory (Azure AD) é um dispositivo de nuvem de gerenciamento de identidade e acesso que fornece serviços de diretório, governança de identidade e gerenciamento de acesso do aplicativo. O AD do Azure rapidamente [permite que o logon único (SSO)](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, 000 pré-integrados aplicativos comerciais e personalizados no hello [Galeria de aplicativos do AD do Azure](https://azure.microsoft.com/marketplace/active-directory/all/). Muitos desses aplicativos você provavelmente já usa, como o Office 365, Salesforce.com, Box, ServiceNow e Workday.

Um único diretório do Azure AD é automaticamente associado a uma assinatura do Azure quando é criado. Como o serviço de identidade Olá no Azure, o AD do Azure, em seguida, fornece todo o gerenciamento de identidade e funções de controle de acesso para recursos baseados em nuvem. Esses recursos podem incluir grupos, aplicativos e usuários para um locatário individual (organização) conforme mostrado no diagrama a seguir de saudação:

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure oferece várias identidades de tooleverage maneiras como um serviço (IDaaS) com vários níveis de complexidade toomeet necessidades da sua organização individuais. restante deste artigo Olá ajuda a compreender a terminologia básica de identidade do Azure e conceitos, bem como recomendações para você toomake Olá melhor escolha entre as opções disponíveis de saudação.

## <a name="terms-tooknow"></a>Tooknow de termos

Antes de decidir em uma solução de identidade do Azure para sua organização, é necessário um entendimento básico de saudação termos usados quando falamos sobre os serviços de identidade do Azure.

|Termo tooknow| Descrição|
|-----|-----|
|Assinatura do Azure |As assinaturas são toopay usado para serviços de nuvem do Azure e cartão de crédito tooa geralmente vinculados. Você pode ter várias assinaturas, mas pode ser difícil tooshare recursos entre assinaturas.|
|Locatário do Azure | Um locatário do Azure AD é representativo de uma única organização. É uma instância dedicada e confiável do Azure AD criada automaticamente quando uma organização inscreve-se para uma assinatura do serviço de nuvem da Microsoft, como Azure, Intune ou Office 365. Os locatários podem obter acesso tooservices em um ambiente dedicado (único Locatário) ou em um ambiente compartilhado com outras organizações (multilocatário).|
|Diretório do AD do Azure | Cada locatário do Azure tem um Azure dedicado, confiável diretório do AD que contém usuários do locatário hello, grupos e aplicativos. Funções de gerenciamento de identidade e acesso tooperform usado para recursos de locatário é. Como um único diretório AD do Azure é provisionado automaticamente toorepresent sua organização quando você se inscreve para um serviço de nuvem da Microsoft como Office 365, Microsoft Intune ou do Azure, você às vezes, verá Olá termos *locatário*, *AD do azure*, e *diretório AD do Azure* usados de maneira intercambiável. |
|Domínio personalizado | Quando você se inscreve pela primeira vez para uma assinatura de serviço de nuvem da Microsoft, seu locatário (organização) usa um nome de domínio *.onmicrosoft.com*. No entanto, a maioria das organizações tem um ou mais nomes de domínio que são usados toodo negócios e que os usuários finais usam tooaccess os recursos da empresa. Você pode adicionar seu nome de domínio personalizado tooAzure AD para que hello nome de domínio é usuários tooyour familiares, como  *alice@contoso.com*  em vez de  *alice@contoso.onmicrosoft.com* . |
|Conta do AD do Azure | Essas são as identidades criadas usando o Azure AD ou outro serviço de nuvem da Microsoft, como o Office 365. Eles são armazenados no AD do Azure e tooany acessível de assinaturas de serviços de nuvem da organização hello. |
|Administrador de assinatura do Azure| o administrador da conta Olá é Olá pessoa inscreveu ou comprou Olá assinatura do Azure. Eles podem usar o hello [Centro de contas](https://account.windowsazure.com/Home/Index) tooperform várias tarefas de gerenciamento, como criar assinaturas, cancelar assinaturas, alterar a cobrança Olá para uma assinatura ou alterar Olá administrador de serviço. |
|Administrador Global do Azure AD | Administradores globais do Azure AD têm recursos administrativos do acesso completo tooall AD do Azure. Olá quem se inscreve para uma assinatura de serviço de nuvem da Microsoft automaticamente se torna um administrador global por padrão. Você pode ter mais de um administrador global, mas apenas administradores globais podem atribuir um dos [Olá outras funções de administrador](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers. |
|Conta da Microsoft | Contas da Microsoft (criadas por você para uso pessoal) fornecem acesso orientado tooconsumer produtos da Microsoft e serviços de nuvem, como o Outlook (Hotmail), OneDrive, Xbox LIVE ou Office 365. Essas identidades são criadas e armazenadas em Olá sistema de conta Microsoft consumidor identidade executado pela Microsoft.|
|Contas corporativas ou de estudante | Contas corporativas ou de Estudante (emitidas por um administrador para uso comercial/acadêmicas) fornecem acesso tooenterprise nível empresarial Microsoft serviços em nuvem, como Azure, o Intune ou o Office 365.|


## <a name="concepts-toounderstand"></a>Conceitos toounderstand

Agora que você sabe os termos de identidade do Azure básico hello, você deve saber mais sobre esses conceitos de identidade do Azure que ajudarão-lo a tomar uma decisão de serviço de informado identidade do Azure.

|Conceito toounderstand |Descrição|
|-----|-----|
|[Como as assinaturas do Azure são associadas ao Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |Cada assinatura do Azure tem uma relação de confiança com um Azure tooauthenticate usuários do AD directory, serviços e dispositivos. *Diretório Olá mesmo Azure AD podem confiar em várias assinaturas, mas uma assinatura confiará apenas um único diretório do Azure AD*. Essa relação de confiança é diferente de relacionamento de saudação que uma assinatura tem com outros recursos do Azure (sites, bancos de dados e assim por diante), que são mais como recursos filho de uma assinatura. Se uma assinatura expira, em seguida, tooresources de acesso associados à assinatura Olá diferente do AD do Azure também interrompe. No entanto, o diretório de saudação do AD do Azure permanece no Azure, para que você possa associar outra assinatura esse diretório e continuar toomanage recursos de locatário.|
|[Como funciona o licenciamento do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | Quando você compra ou ativar o Enterprise Mobility Suite, Azure AD Premium ou Azure AD Basic, seu diretório é atualizado com assinatura hello, incluindo o período de validade e pago licenças. Depois que a assinatura Olá estiver ativa, serviço Olá pode ser gerenciado por administradores globais do AD do Azure e usado por usuários licenciados. As informações de assinatura, incluindo o número de saudação de licenças atribuídas ou disponíveis, estão disponíveis no hello portal do Azure de saudação **Active Directory do Azure** > **licenças** folha. Isso também é Olá melhor toomanage de local de suas atribuições de licença.|
|[Controle de acesso baseado em função no hello portal do Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|O Azure RBAC (controle de acesso baseado em função) fornece o gerenciamento de acesso refinado para os recursos do Azure. Número excessivo de permissões pode expor e tooattackers da conta. Permissões insuficientes fazem com que os funcionários não consigam trabalhar com eficiência. Usando o RBAC, você pode dar a funcionários Olá permissões exatas necessárias com base em três funções básicas que se aplicam a grupos de recursos tooall: leitor, colaborador, proprietário. Você também pode criar backup too2, 000 seus próprios [funções personalizadas de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) toomeet suas necessidades específicas. |
|[Identidade híbrida](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|Identidade híbrida é obtida integrando seu Windows Server Active Directory (AD DS) local com o Azure AD usando o [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Isso permite que você tooprovide uma identidade comum para os usuários do Office 365, Azure e aplicativos locais ou aplicativos SaaS integrada ao AD do Azure. Com identidade híbrida, você efetivamente estender seus locais nuvem toohello ambiente identidades e acesso.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>diferença de saudação entre o Windows Server AD DS e AD do Azure
Tanto o Azure AD (Azure Active Directory) quanto o Active Directory (Active Directory Domain Services ou AD DS) local são sistemas que armazenam dados de diretório e gerenciam a comunicação entre usuários e recursos, incluindo processos de logon do usuário, autenticação e pesquisas de diretório.

Se você já estiver familiarizado com local Windows Server Active Directory serviços de domínio (AD DS), introduzida no Windows 2000 Server, em seguida, você provavelmente já conhece o conceito básico de saudação de um serviço de identidade. No entanto, também é importante toounderstand AD do Azure não é apenas um controlador de domínio na nuvem hello. É uma nova maneira de fornecer identidade como um serviço (IDaaS) no Azure que requer uma nova maneira de recursos de baseado em nuvem de adoção do pensamento toofully e proteger sua organização contra ameaças modernas. 

O AD DS é uma função de servidor no Windows Server, o que significa que ele pode ser implantado em máquinas físicas ou virtuais. Ele tem uma estrutura hierárquica baseada em X.500. Ele usa o DNS para localizar objetos, usa basicamente Kerberos para autenticação e é possível interagir com ele usando LDAP. Active Directory permite OUs (unidades organizacionais) e objetos de diretiva de grupo (GPOs) toojoining domínio de toohello de máquinas e relações de confiança são criadas entre domínios.

A TI protegeu seu perímetro de segurança por anos usando o AD DS, mas empresas modernas sem perímetro que dão suporte a necessidades de identidade para funcionários, clientes e parceiros precisam de um novo plano de controle. O Azure AD é esse plano de controle de identidade. Segurança foi movido para fora de nuvem de toohello do firewall corporativo Olá onde o AD do Azure protege os recursos da empresa e acesso, fornecendo uma identidade comum para os usuários (no local ou na nuvem Olá). Isso permite que seu toosecurely de flexibilidade Olá usuários acesso Olá aplicativos precisam tooget seu trabalho de praticamente qualquer dispositivo. Controles de proteção contínua de dados com base em risco, com o apoio de recursos de aprendizado de máquina e relatórios detalhados, também são fornecidos para essa empresa tookeep de necessidades de TI dados seguros.

O Azure AD é um serviço de diretório público para vários clientes, o que significa que dentro dele é possível criar um locatário para seus servidores e aplicativos de nuvem, como o Office 365. Usuários e grupos são criados em uma estrutura simples sem OUs ou GPOs. A autenticação é realizada por meio de protocolos como SAML, WS-Federation e OAuth. É possível tooquery AD do Azure, mas em vez de usar LDAP, você deve usar uma API de REST chamada de API gráfica do AD. Todos eles usam HTTP e HTTPS.

### <a name="extend-office-365-management-and-security-capabilities"></a>Estender as capacidades de gerenciamento e segurança do Office 365
Já está usando o Office 365? Você pode acelerar a transformação digital estendendo recursos internos do Office 365 com o AD do Azure toosecure todos os seus recursos, habilitando produtividade segura para sua força de trabalho inteira. Quando você usar o AD do Azure, além de recursos tooOffice 365, você pode proteger seu portfólio de todo o aplicativo com uma identidade que habilita logon único para todos os aplicativos. Você pode expandir os recursos de acesso condicional com base não apenas no estado do dispositivo, como também em usuário, local, aplicativo e risco. As capacidades de MFA (Autenticação Multifator) fornecem ainda mais proteção quando necessário. Você obterá supervisão adicional de privilégios do usuário e fornecerá acesso administrativo sob demanda just-in-time. Os usuários sejam mais produtivos e criar menos tíquetes de assistência técnica, recursos de auto-atendimento de toohello Obrigado AD do Azure fornece como redefinir senhas esquecidas, solicitações de acesso do aplicativo e criar e gerenciar grupos.

> [!TIP]
> Deseja toolearn mais sobre como usar o gerenciamento de identidades do AD do Azure com o Office 365? [Obter o livro eletrônico Olá](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html).

## <a name="microsoft-azure-identity-solutions"></a>Soluções de identidade do Microsoft Azure

O Microsoft Azure oferece várias toomanage de maneiras identidades dos usuários se eles são mantidos totalmente no local, somente em Olá nuvem, ou até mesmo em algum lugar entre. Essas opções incluem: AD DS do tipo DIY (faça você mesmo) no Azure, Azure AD (Azure Active Directory), Identidade Híbrida e Azure AD Domain Services.

### <a name="do-it-yourself-diy-ad-ds"></a>AD DS do tipo DIY (faça você mesmo)
Para empresas que precisam apenas uma superfície pequena na nuvem hello, **tipo faça você mesmo (DIY) AD DS** no Azure pode ser usado. Essa opção dá suporte a vários cenários do Windows Server AD DS apropriados para implantação como VMs (máquinas virtuais) no Azure. Por exemplo, você pode criar uma VM do Azure como um controlador de domínio em execução em um datacenter longínqua que está conectada toohello remotos da rede. A partir daí, Olá VM seria capaz de toosupport solicitações de autenticação de usuários remotos e melhorar o desempenho de autenticação. Essa opção também é bem-apropriado como um substituto de custo relativamente baixo toootherwise sites desastres muito caros recuperação hospedando um número pequeno de controladores de domínio e uma única rede virtual no Azure. Por fim, talvez você precise toodeploy um aplicativo no Azure, como o SharePoint, o que requer o Windows Server AD DS, mas não tem nenhuma dependência na rede de local de saudação ou Olá corporativa Windows Server Active Directory. Nesse caso, você pode implantar uma floresta isolada de requisitos do farm de servidores do SharePoint Olá toomeet do Azure. Também tem suporte para aplicativos de rede toodeploy que exigem a rede de local de toohello de conectividade e saudação do Active Directory local.

### <a name="azure-active-directory-azure-ad"></a>Active Directory do Azure (Azure AD)
O **Azure AD autônomo** é uma solução de IDaaS (identidade e gerenciamento de acesso como um serviço) totalmente baseada em nuvem. O AD do Azure fornece um conjunto robusto de recursos toomanage usuários e grupos. Ele ajuda a proteger o acesso local tooon e aplicativos, inclusive serviços web do Microsoft como Office 365 e muitos softwares da Microsoft como um aplicativo de serviço (SaaS) na nuvem. O Azure AD é fornecido em três edições: Gratuita, Básica e Premium. O AD do Azure aumenta a eficácia organizacional e aumenta a segurança além Olá perímetro firewall tooa novo plano de controle protegida pelo aprendizado de máquina do Azure e outros recursos de segurança avançados.

### <a name="hybrid-identity"></a>Identidade híbrida
Em vez de escolher entre soluções de identidade baseados em nuvem ou local, muitos CIOs e empresas, que começaram a antecipando a direção de longo prazo da sua empresa, de visão são estender seus locais de nuvem toohello diretórios **identidade híbrida** soluções. Com identidade híbrida, você receberá uma identidade realmente global e solução de gerenciamento de acesso que fornece acesso seguro e produtivo toohello aplicativos os usuários precisam toodo seus trabalhos.

> [!TIP]
> toolearn mais sobre como CIOs fez uma parte central de suas estratégias de TI, ao Active Directory do Azure download Olá [tooAzure de guia do CIO do Active Directory](https://aka.ms/AzureADCIOGuide).

### <a name="azure-ad-domain-services"></a>Azure AD Domain Services
**Serviços de domínio do AD do Azure** fornece um toouse baseado em nuvem opção AD DS para controle leve de configuração de máquina virtual do Azure e uma maneira toomeet requisitos de identidade local para teste e desenvolvimento de aplicativo de rede. Serviços de domínio do AD do Azure não é toolift e seu local de deslocamento para a infraestrutura de AD DS tooAzure VMs gerenciados pelos serviços de domínio do AD do Azure. Em vez disso, hello Azure VMs em domínios gerenciados deve ser usado toosupport Olá desenvolvimento, teste e movimentação de aplicativos locais que exigem a nuvem de toohello de métodos de autenticação de AD DS.

## <a name="common-scenarios-and-recommendations"></a>Cenários e recomendações comuns

Aqui estão alguns cenários comuns de identidade e acesso com recomendações como toowhich opção identidade do Azure pode ser mais apropriada para cada um.

|Cenário de identidade| Recomendações|
|-----|-----|
|Minha organização fez grandes investimentos em local no Windows Server Active Directory, mas queremos tooextend nuvem de toohello de identidade.| solução de identidade do Azure Olá usado amplamente é [identidade híbrida](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Se você já fez investimentos locais AD DS, você pode estender facilmente nuvem toohello de identidade usando o Azure AD Connect.|
|Minha empresa nasceu em nuvem hello e não temos nenhum investimentos em soluções de identidade local.| [Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) é a melhor opção hello para empresas somente em nuvem, sem nenhum investimentos locais.|
|Preciso leve VM do Azure configuração e controle toomeet identidade requisitos de local para teste e desenvolvimento de aplicativo.|[Serviços de domínio do AD do Azure](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) é uma boa opção se você precisa toouse AD DS para controle de configuração de máquina virtual do Azure leve ou busca toodevelop ou migra de nuvem de toohello aplicativos herdados, com reconhecimento de diretório local.|  
|Preciso toosupport algumas máquinas virtuais no Azure, mas minha empresa é investida ainda muito no local no Active Directory (AD DS).|Use [DIY AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse VMs do Azure quando você precisar toosupport algumas máquinas virtuais e tiver grandes AD DS investimentos no local. |

## <a name="where-can-i-learn-more"></a>Onde posso saber mais?
Temos inúmeras ótimos recursos toohelp online que você saiba tudo sobre o AD do Azure. Aqui está uma lista de artigos excelente tooget iniciar:

* [Habilitando seu diretório para gerenciamento híbrido com o Azure AD Connect](active-directory-aadconnect.md)
* [Segurança adicional para um mundo sempre conectado](../multi-factor-authentication/multi-factor-authentication.md)
* [Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](active-directory-saas-app-provisioning.md)
* [Introdução aos Relatórios do AD do Azure](active-directory-reporting-getting-started.md)
* [Gerenciar suas senhas de qualquer lugar](active-directory-passwords.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](active-directory-saas-app-provisioning.md)
* [Como tooprovide proteger o acesso remoto aplicativos tooon locais](active-directory-application-proxy-get-started.md)
* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [O que é o licenciamento do Active Directory do Microsoft Azure?](active-directory-licensing-what-is.md)
* [Como descobrir aplicativos na nuvem não aprovados, usados em minha organização](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>Próximas etapas

Agora que você entende conceitos de identidade do Azure e Olá opções disponíveis tooyou, você pode usar o hello recursos tooget iniciado implementação Olá opção escolhida a seguir:

[Saiba mais sobre as soluções de identidade híbridas do Azure](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[Saiba mais em um ambiente de prova de conceito do Azure](https://aka.ms/aad-poc)

[Implantar o Azure AD em produção](https://aka.ms/aad-onboard)
