---
title: aaaFundamentals do gerenciamento de identidades do Azure | Microsoft Docs
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Fundamentos do gerenciamento de identidades do Azure
Dinâmica com mais recursos de digital da empresa fora da rede corporativa hello, na nuvem hello e em dispositivos, uma solução excelente de gerenciamento de identidade e acesso baseado em nuvem está se tornando uma necessidade. Identidades baseadas em nuvem agora são melhor controle de toomaintain de maneira Olá over e visibilidade sobre como e quando os usuários acessar aplicativos e dados corporativos.

Microsoft tem sido protegendo identidades baseado em nuvem para mais de uma década e agora, com [do Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), esses mesmos sistemas de proteção são tooyou disponível. Com o Azure AD, os administradores de empresa podem garantir facilmente a responsabilidade do usuário e do administrador com mais segurança e controle do que nunca.

O Azure AD Premium é uma baseado em nuvem de identidade e acesso solução de gerenciamento com recursos avançados de proteção que permite que uma identidade de segurança para todos os aplicativos, proteção de identidade (aprimorada por Olá [gráfico de segurança do Microsoft intelligence](https://www.microsoft.com/en-us/security/intelligence)) e o gerenciamento de identidade com privilégios. Outro não apenas monitoramento ou ferramenta, de relatório do Azure AD Premium pode proteger as identidades do usuário em tempo real e habilitar você toocreate acesso com base em risco, adaptável políticas tooprotect dados da sua organização.

Assista a este vídeo curto para obter uma visão geral da proteção e do gerenciamento de identidades do Azure AD:
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

A Microsoft não apenas fornece uma identidade que usa todos os locais, mas também um conjunto de ferramentas tooautomate, ajudar a proteger e gerenciar IT dentro da sua organização. Mesmo após o surgimento de saudação de computação em nuvem, há ainda exigem toomanage e controlar tarefas de TI, como o suporte técnico chama tooreset senhas de usuário, o usuário grupo gerenciamento e solicitações do aplicativo. Complicar as coisas ainda mais, os funcionários estão agora levando toowork seus dispositivos pessoais e usando aplicativos de SaaS prontamente disponíveis. Isso torna mantêm o controle sobre seus aplicativos em plataformas de nuvem pública e data centers corporativos um desafio significativo.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Conectar-se o Active Directory no local com o Azure AD e Office 365
As organizações que fizeram grandes investimentos no Active Directory no local podem estender a nuvem de toohello os investimentos integrando seus diretórios locais com o AD do Azure em [gerenciamento de identidade híbrida](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Isso torna os usuários mais produtivos fornecendo uma identidade comum para acessar recursos, independentemente do local. Os usuários e as organizações podem usar logon único (SSO) tooaccess recursos locais e na nuvem serviços como o Office 365.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) é Olá única ferramenta que precisa de integração de saudação do tooget feita. Conexão do AD do Azure fornece recursos toosupport sua sincronização de identidades precisa e substitui as versões anteriores das ferramentas de integração de identidade como DirSync e sincronização do AD do Azure. Com o Azure AD Connect, gerenciamento de identidade e a sincronização entre local e o Azure AD é habilitado por meio de:

- Sincronização - esse componente é responsável pela criação de usuários, grupos e outros objetos. Também é responsável por garantir que as informações de identidade para os usuários locais e grupos correspondentes nuvem hello. Write-back de senha também pode ser habilitado tookeep nos diretórios locais em sincronia quando um usuário atualiza sua senha no AD do Azure.
- O AD FS - federação é um recurso opcional fornecido pelo Azure AD Connect que pode ser usado tooconfigure um ambiente híbrido usando um local infraestrutura do AD FS. Federação pode ser usada por organizações tooaddress complexas as implantações, como logon único, a imposição de AD política e o cartão inteligente ou de terceiros MFA.
- Monitoramento de integridade - [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) pode fornecer monitoramento robusto e fornecer um local central, Olá tooview portal do Azure essa atividade.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Aumentar a produtividade e reduzir os custos de assistência técnica com um únicos e autoatendimento experiências de logon

Os funcionários são mais produtivos quando eles têm um único tooremember de nome de usuário e senha e uma experiência consistente de cada dispositivo. Também salvarem tempo quando eles podem executar tarefas de autoatendimento como [redefinir uma senha esquecida](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) ou solicitando acesso tooan aplicativo sem aguardar a assistência do suporte técnico de saudação.

O AD do Azure [estende o Active Directory no local](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) em nuvem hello, permitindo que usuários toouse sua conta institucional primária para seus dispositivos ingressados no domínio, os recursos da empresa e todos os Olá web e aplicativos SaaS eles necessário toouse tooget seus trabalhos. Além disso toonot ter tooremember vários conjuntos de nomes de usuário e senhas, acesso de aplicativo dos usuários podem também ser automaticamente provisionados (ou eliminação provisionados) com base em suas associações de grupo da organização e seu status como um funcionário. E você pode controlar o acesso para aplicativos de galeria ou para seus próprios aplicativos de locais que você tiver desenvolvido e publicados por meio de saudação [Proxy de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Gerenciar e controlar os recursos de toocorporate de acesso
Microsoft identidade e acesso de gerenciamento ajudam a soluções TI proteger acesso tooapplications e recursos em datacenter corporativo hello e em nuvem Olá, habilitando níveis adicionais de validação, como [aautenticaçãomultifator](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) e [políticas de acesso condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). O monitoramento de atividade suspeita por meio de alertas, auditoria e relatórios de segurança avançados ajuda a reduzir potenciais problemas de segurança.

Políticas de acesso condicional no Azure AD Premium oferecem, Olá administrador corporativo, Olá regras de acesso baseado em políticas de toocreate de capacidade para qualquer aplicativo do Azure AD conectado (aplicativos SaaS, aplicativos personalizados executados em aplicativos de web de nuvem ou local de saudação). O AD do Azure avalia essas políticas em tempo real e impõe-los sempre que um usuário tenta tooaccess um aplicativo. Políticas de proteção de identidade do Azure permitem que você execute a ação tooautomatically se uma atividade suspeita é descoberta. Essas ações podem incluir bloqueando o acesso toousers em risco, aplicar a autenticação multifator, e redefinindo as senhas se ele se parece com as credenciais do usuário foram comprometidas.


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Privileged Identity Management

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), incluído com hello Azure Active Directory Premium P2 oferta, permite que você toodiscover, restringir e monitorar contas administrativas e seus tooresources de acesso no seu Active Directory do Azure e outros Serviços online da Microsoft. Ele também ajuda a administrar o acesso administrativo sob demanda por Olá exata período que é necessário.

Privileged Identity Management pode impor os direitos de administrador sob demanda para que os administradores possam solicitar elevação de autenticado, temporária multifator de seus privilégios pré-configurado em períodos de tempo antes que suas contas retornam tooa normal estado do usuário.

## <a name="benefits-of-azure-identity"></a>Benefícios da Identidade do Azure

Com o gerenciamento de identidades do Azure, você pode:

-   Criar e gerenciar uma identidade única para cada usuário em toda a sua empresa, mantendo os usuários, grupos e dispositivos em sincronia com o [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Fornecer acesso de logon único tooyour aplicativos incluindo milhares de aplicativos SaaS pré-integrados ou fornecer acesso remoto seguro a aplicativos SaaS de tooon local usando Olá [Proxy de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Habilitar segurança de acesso do aplicativo por meio da aplicação da [autenticação multifator](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) com base em regras para aplicativos locais e na nuvem.

-   Aumentar a produtividade do usuário com [de redefinição de senha de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)e o grupo e o aplicativo acessar solicitações usando Olá [portal MyApps](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Aproveitar Olá [alta disponibilidade e confiabilidade](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) de um empresariais em todo o mundo, solução de gerenciamento de identidade e acesso baseado em nuvem.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre as soluções de identidade do Azure](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)