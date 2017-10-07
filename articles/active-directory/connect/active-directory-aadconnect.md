---
title: Conectar o Active Directory com o Azure Active Directory. | Microsoft Docs
description: "O Azure AD Connect integrará seus diretórios locais com o Azure Active Directory.  Isso permite que você tooprovide uma identidade comum para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure."
keywords: "Introdução tooAzure AD Connect, visão geral do Azure AD Connect, o que é o Azure AD Connect, do active directory de instalação"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Integrar seus diretórios locais no Azure Active Directory
O Azure AD Connect integrará seus diretórios locais com o Azure Active Directory.  Isso permite que você tooprovide uma identidade comum para os usuários para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure. Este tópico orientará você Olá planejamento, implantação e etapas da operação. É uma coleção de links toohello tópicos relacionados toothis área.

> [!IMPORTANT]
> [Conexão do AD do Azure é Olá tooconnect de maneira melhor seu diretório local com o Azure AD e Office 365. Este é um tooAzure de tooupgrade bastante AD Connect de sincronização de diretório ativo (DirSync) do Windows Azure ou Azure AD Sync, essas ferramentas são preteridos-los agora e chegará ao fim do suporte em 13 de abril de 2017.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![O que é o Azure AD Connect](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Por que usar o Azure AD Connect
A integração de seus diretórios locais ao AD do Azure torna os usuários mais produtivos ao fornecer uma identidade comum para acesso aos recursos na nuvem e locais. Usuários e organizações podem aproveitar a seguir hello:

* Os usuários podem usar aplicativos de locais de tooaccess uma única identidade e serviços como o Office 365 em nuvem.
* A única ferramenta tooprovide uma experiência de implantação fácil de sincronização e entrar.
* Fornece recursos mais recentes do Olá para seus cenários. O Azure AD Connect substitui as versões mais antigas das ferramentas de integração de identidade, como DirSync e Azure AD Sync. Para saber mais, confira [Comparação das ferramentas de integração de diretórios de Identidade Híbrida](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Como o Azure AD Connect funciona
Azure Active Directory Connect é composto por três componentes principais: serviços de sincronização hello, o componente de serviços de Federação do Active Directory opcional hello e o componente de monitoramento Olá denominado [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Pilha do Azure AD Connect](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Sincronização - esse componente é responsável pela criação de usuários, grupos e outros objetos. Também é responsável por garantir que as informações de identidade para os usuários locais e grupos correspondentes nuvem hello.
* O AD FS - federação é uma parte opcional da conexão do AD do Azure e pode ser usado tooconfigure um ambiente híbrido usando um local infraestrutura do AD FS. Isso pode ser usado por organizações tooaddress complexas as implantações, como ingresso no domínio SSO, imposição de AD política e o cartão inteligente ou 3ª parte MFA.
* Monitoramento de integridade - Azure AD Connect Health pode fornecer monitoramento robusto e fornecer um local central, Olá tooview portal do Azure essa atividade. Para obter informações adicionais, consulte [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Instalar o Azure AD Connect
Você pode encontrar o download de saudação para o Azure AD Connect em [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).

| Solução | Cenário |
| --- | --- |
| Antes de iniciar: [Hardware e pré-requisitos](active-directory-aadconnect-prerequisites.md) |<li>Toocomplete etapas antes de iniciar tooinstall do Azure AD Connect.</li> |
| [Configurações Expressas](active-directory-aadconnect-get-started-express.md) |<li>Se você tiver uma única floresta do AD, em seguida, isso Olá recomenda toouse opção.</li> <li>Usuário entrar com hello mesmo senha usando a sincronização de senha.</li> |
| [Configurações personalizadas](active-directory-aadconnect-get-started-custom.md) |<li>Usadas quando você tem várias florestas. Dá suporte a várias [topologias](active-directory-aadconnect-topologies.md) locais.</li> <li>Personalize sua opção de entrada, como o ADFS para federação, ou use um provedor de identidade de terceiros.</li> <li>Personalize os recursos de sincronização, como filtragem e write-back.</li> |
| [Atualização do DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Usado quando você tem um servidor DirSync existente já em execução.</li> |
| [Atualizar do Azure AD Sync ou do Azure AD Connect](active-directory-aadconnect-upgrade-previous-version.md) |<li>Há vários métodos diferentes, dependendo de sua preferência.</li> |

[Após a instalação](active-directory-aadconnect-whats-next.md) deve verificar se ele está funcionando conforme o esperado e atribuir licenças a usuários toohello.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Próximas etapas tooInstall do Azure AD Connect
|Tópico |Link|  
| --- | --- |
|Baixar o Azure AD Connect | [Baixar o Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Instalar usando as Configurações expressas | [Instalação expressa do Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Instalar usando Configurações personalizadas | [Instalação personalizada do Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Atualização do DirSync | [Atualizar a partir da ferramenta de sincronização do AD do Azure (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Após a instalação | [Verificar a instalação do hello e atribuir licenças](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Saiba mais sobre como instalar o Azure AD Connect
Você também deseja tooprepare para [operacionais](active-directory-aadconnectsync-operations.md) preocupações. Talvez você queira toohave um servidor de espera para que você facilmente pode cair se houver um [desastres](active-directory-aadconnectsync-operations.md#disaster-recovery). Se você planejar alterações de configuração frequentes toomake, você deve planejar um [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode) server.

|Tópico |Link|  
| --- | --- |
|Topologias com suporte | [Topologias para o Azure AD Connect](active-directory-aadconnect-topologies.md)|
|Conceitos de design | [Conceitos de design do Azure AD Connect](active-directory-aadconnect-design-concepts.md)|
|Contas usadas para instalação | [Mais informações sobre permissões e as credenciais de Conexão do AD do Azure](./active-directory-aadconnect-accounts-permissions.md)|
|Planejamento operacional | [Sincronização do Azure AD Connect: considerações e tarefas operacionais](active-directory-aadconnectsync-operations.md)|
|Opções de entrada de usuário | [Opções de entrada de usuário do Azure AD Connect](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Configurar recursos de sincronização
O Azure Connect AD vem com vários recursos que você pode ativar opcionalmente ou que estão habilitados por padrão. Em alguns casos, alguns recursos podem exigir uma configuração adicional em certos cenários e topologias.

[Filtragem](active-directory-aadconnectsync-configure-filtering.md) é usado quando você deseja toolimit quais objetos estão sincronizados tooAzure AD. Por padrão, todos os usuários, contatos, grupos e computadores Windows 10 são sincronizados. Você pode alterar a saudação filtragem com base em atributos, unidades organizacionais ou domínios.

[Sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) sincroniza o hash de senha Olá no Active Directory tooAzure AD. usuário final de saudação pode usar Olá a mesma senha local e na nuvem Olá mas apenas gerenciá-lo em um local. Já que ele usa o Active Directory no local como autoridade hello, você também pode usar sua própria política de senha.

[Write-back de senha](../active-directory-passwords-getting-started.md) permitir toochange seus usuários e redefinir suas senhas na nuvem hello e ter sua política de senha local aplicada.

[Write-back de dispositivo](active-directory-aadconnect-feature-device-writeback.md) permitirá que um dispositivo registrado no AD do Azure toobe gravado do Active Directory local tooon para que possa ser usado para acesso condicional.

Olá [impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) recurso é ativado por padrão e protege seu diretório na nuvem de vários exclusões no hello simultaneamente. Por padrão, ele permite 500 exclusões por execução. Você pode alterar essa configuração, dependendo do tamanho de sua organização.

[A atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) é habilitado por padrão para instalações de configurações expressas e garante que o Azure AD Connect está sempre toodate com a versão mais recente do hello.

### <a name="next-steps-tooconfigure-sync-features"></a>Recursos de sincronização de tooconfigure etapas Avançar
|Tópico |Link|  
| --- | --- |
|Configurar a filtragem | [Sincronização do Azure AD Connect: configurar a filtragem](active-directory-aadconnectsync-configure-filtering.md)|
|Sincronização de senhas | [Azure AD Connect Sync: implementar a sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md)|
|write-back de senha | [Introdução ao gerenciamento de senhas](../active-directory-passwords-getting-started.md)|
|write-back do dispositivo | [Habilitando write-back de dispositivo no Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md)|
|impedir exclusões acidentais | [Sincronização do Azure AD Connect: impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|Atualização automática | [Azure AD Connect: Atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Personalizar a sincronização do Azure AD Connect
Sincronização do Azure AD Connect vem com uma configuração padrão que é toowork desejado para a maioria dos clientes e topologias. Mas sempre há situações em que a configuração padrão de saudação não funciona e deve ser ajustada. É alterado de toomake com suporte como documentadas nesta seção e tópicos vinculados.

Se você não tiver trabalhado com uma topologia de sincronização antes de ser Noções básicas do toostart toounderstand hello e Olá termos usados conforme descrito em hello [conceitos técnicos](active-directory-aadconnectsync-technical-concepts.md). Conexão do AD do Azure é a evolução de saudação do MIIS2003, ILM2007 e FIM2010. Mesmo que algumas coisas sejam idênticas, também houve muitas mudanças.

Olá [configuração padrão](active-directory-aadconnectsync-understanding-default-configuration.md) supõe que pode haver mais de uma floresta na configuração de saudação. Nessas topologias, um objeto de usuário pode ser representado como um contato em outra floresta. usuário Olá também pode ter uma caixa de correio vinculada em outra floresta de recursos. comportamento de saudação da configuração padrão de saudação é descrito em [usuários e contatos](active-directory-aadconnectsync-understanding-users-and-contacts.md).

modelo de configuração de saudação em sincronia é chamado [provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Olá fluxos de atributo avançadas estiver usando [funções](active-directory-aadconnectsync-functions-reference.md) tooexpress atributo transformações. Você pode ver e examinar Olá toda configuração usando as ferramentas que vem com o Azure AD Connect. Se você precisar de alterações de configuração de toomake, certifique-se de seguir Olá [práticas recomendadas](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) é mais fácil tooadopt novas versões.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Próximas etapas toocustomize AD do Azure Connect sincronização
|Tópico |Link|  
| --- | --- |
|Todos os artigos sobre a sincronização do Azure AD Connect | [Sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md)|
|conceitos técnicos | [Sincronização do Azure AD Connect: conceitos técnicos](active-directory-aadconnectsync-technical-concepts.md)|
|Compreendendo a configuração padrão da saudação | [Sincronização do Azure AD Connect: Compreendendo a configuração padrão da saudação](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Noções básicas sobre usuários e contatos | [Azure AD Connect Sync: noções básicas sobre usuários e contatos](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|provisionamento declarativo | [Azure AD Connect Sync: noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Alteração da configuração saudação padrão | [Práticas recomendadas para alterar a configuração padrão de saudação](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Configurar recursos de federação
AD FS podem ser configurado toosupport [vários domínios](active-directory-aadconnect-multiple-domains.md). Por exemplo, você pode ter vários domínios superiores é necessário toouse para federação.

Se o servidor do AD FS não foi configurado tooautomatically atualizar certificados do AD do Azure ou se você usar uma solução não ADFS, em seguida, você será notificado quando você tem muito[atualizar certificados](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Recursos de Federação do próximos etapas tooconfigure
|Tópico |Link|  
| --- | --- |
|Todos os artigos do AD FS | [Azure AD Connect e federação](active-directory-aadconnectfed-whatis.md)|
|Configurar o ADFS com subdomínios | [Suporte a Vários Domínios para Federação com o Azure AD](active-directory-aadconnect-multiple-domains.md)|
|Gerenciar o farm do AD FS | [Gerenciamento do AD FS e personalização com o Azure AD Connect](active-directory-aadconnect-federation-management.md)|
|Atualização manual dos certificados de federação | [Renovando certificados de federação para o Office 365 e AD do Azure](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Mais informações e referências
|Tópico |Link|  
| --- | --- |
|Histórico de versão | [Histórico de versão](active-directory-aadconnect-version-history.md)|
|Comparar o DirSync, Azure ADSync e o Azure AD Connect | [Comparação de ferramentas de integração de diretório](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Lista de compatibilidade de soluções não ADFS para o AD do Azure | [Lista de compatibilidade de federação do AD do Azure](active-directory-aadconnect-federation-compatibility.md)|
|Configurando um Idp do SAML 2.0|[Usando um provedor de identidade (Idp) do SAML 2.0 para o logon único](active-directory-aadconnect-federation-saml-idp.md)|
|Atributos sincronizados | [Atributos sincronizados](active-directory-aadconnectsync-attributes-synchronized.md)|
|Monitorando com o Azure AD Connect Health | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|Perguntas frequentes | [Perguntas frequentes do Azure AD Connect](active-directory-aadconnect-faq.md)|

**Recursos adicionais**

Acender 2015 apresentação sobre como estender a sua nuvem de toohello diretórios locais.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

