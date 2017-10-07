---
title: "aaaAzure do Active Directory de prova de conceito blocos de construção de guia estratégico | Microsoft Docs"
description: "Explorar e implementar rapidamente os cenários de Identidade e Gerenciamento de Acesso"
services: active-directory
keywords: azure active directory, cartilha, Prova de Conceito, PoC
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Guia estratégico de prova de conceito do Azure Active Directory: blocos de construção

## <a name="catalog-of-roles"></a>Catálogo de funções

| Função | Descrição | Responsabilidade da PoC (prova de conceito) |
| --- | --- | --- |
| **Arquitetura de Identidade / equipe de desenvolvimento** | Essa equipe geralmente é Olá um que projeta solução hello, implementa protótipos, aprovações de unidades e finalmente entrega toooperations | Eles oferecem ambientes hello e Olá aqueles avaliando Olá diferentes cenários da perspectiva da capacidade de gerenciamento de saudação |
| **Equipe de Operações de Identidade Local** | Gerencia Olá identidade diferentes fontes locais: florestas do Active Directory, diretórios LDAP, sistemas de RH e provedores de identidade de Federação. | Fornece acesso local tooon recursos necessários para Olá PoC cenários.<br/>Devem interferir o mínimo possível|
| **Técnicos Proprietários do Aplicativo** | Proprietários técnicos de saudação nuvem de diferentes aplicativos e serviços que integram-se ao AD do Azure | Fornecer detalhes sobre aplicativos SaaS (potencialmente instâncias para teste) |
| **Administrador Global do AD do Azure** | Gerencia a configuração de saudação do AD do Azure | Forneça credenciais de serviço de sincronização de saudação tooconfigure. Geralmente, Olá mesma equipe de arquitetura de identidade durante PoC mas separado durante a fase de operações de saudação|
| **Equipe do Banco de Dados** | Proprietários de infraestrutura de banco de dados de saudação | Fornece o ambiente de tooSQL de acesso (AD FS ou do Azure AD Connect) para executar os preparativos cenário específico.<br/>Devem interferir o mínimo possível |
| **Equipe de Rede** | Proprietários de infraestrutura de rede Olá | Fornecer acesso necessário no nível de rede Olá para sincronização Olá servidores tooproperly acessar Olá fontes de dados e serviços de nuvem (regras de firewall, portas abertas, regras de IPSec etc.) |
| **Equipe de segurança** | Define a estratégia de segurança hello, analisa os relatórios de segurança de várias fontes e acompanha nas descobertas. | Fornecer cenários de avaliação de segurança de destino |

## <a name="common-prerequisites-for-all-building-blocks"></a>Pré-requisitos comuns a todos os blocos de construção

A seguir, estão alguns pré-requisitos necessários para qualquer prova de conceito com o Azure AD Premium.

| Pré-requisito | Recursos |
| --- | --- |
| Locatário Azure AD definido com uma assinatura Azure válida | [Como tooget um Active Directory do Azure locatário](active-directory-howto-tenant.md)<br/>**Observação:** se você já tiver um ambiente com licenças do Azure AD Premium, você pode obter uma assinatura de cap zero navegando toohttps://aka.ms/accessaad <br/>Saiba mais em: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ and https://technet.microsoft.com/library/dn832618.aspx |
| Domínios definidos e verificados | [Adicionar um nome de domínio personalizado tooAzure do Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Observação:** algumas cargas de trabalho, como o Power BI pode ter provisionado um locatário do AD do azure em Olá abrange. toocheck se um determinado domínio é associado tooa locatário, navegue toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Se você obtiver uma resposta bem-sucedida, e o domínio Olá já está atribuído a tooa locatário e assume pode ser necessárias. Nesse caso, contate a Microsoft para obter mais orientações. Saiba mais sobre opções de tomada de saudação em: [o que é a inscrição de autoatendimento do Azure?](active-directory-self-service-signup.md) |
| Avaliação do Azure AD Premium ou EMS habilitada | [Azure Active Directory Premium gratuito por um mês](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Você atribuiu licenças do Azure AD Premium ou EMS tooPoC usuários | [Licencie a si mesmo e seus usuários no Azure Active Directory](active-directory-licensing-get-started-azure-portal.md) |
| Credenciais de Administrador Global do Azure AD | [Atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Opcional mas altamente recomendável: ambiente de laboratório paralelo como um fallback | [Pré-requisitos do Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Sincronização de diretórios - PHS (sincronização de hash de senha) - nova instalação

Aproximar tempo tooComplete: uma hora para menos de 1.000 usuários de PoC

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| TooRun do servidor do Azure AD Connect | [Pré-requisitos do Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Direcionar usuários POC Olá mesmo domínio e é parte de um grupo de segurança e UO | [Instalação personalizada do Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Recursos do Azure AD conectar necessários para Olá POC são identificados | [Conectar o Active Directory com o Azure Active Directory - Configurar recursos de sincronização](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Você precisou de credenciais para ambientes de nuvem e locais  | [Azure AD Connect: Contas e permissões](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Baixar a versão mais recente de saudação do Azure AD Connect | [Baixe o Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Instalar o Azure AD Connect com caminho mais simples de saudação: Express <br/>1. Filtro de tempo de ciclo de sincronização de saudação toohello destino OU toominimize<br/>2. Escolha o conjunto de destino de usuários no grupo local de saudação.<br/>3. Implantar recursos Olá necessários Olá por outros temas de POC | [Azure AD Connect: Instalação personalizada: Filtragem de domínio/UO](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Instalação personalizada: Filtragem baseada no grupo](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Integrando suas identidades locais com o Azure Active Directory: Configurar Recursos de Sincronização](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Abra hello Azure AD Connect da interface do usuário e consulte Olá executando perfis concluída (importar, sincronização e exportar) | [Sincronização do Azure AD Connect: Agendador](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Olá abrir [portal de gerenciamento do Azure AD](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), vá toohello folha de "Todos os usuários", adicionar coluna de "Origem de autoridade" e consulte usuários Olá aparecerem, corretamente marcadas como sendo proveniente de "Windows Server AD" | [Portal de gerenciamento do Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Considerações

1. Examinar as considerações de segurança Olá sincronização de hash de senha [aqui](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Se a sincronização de hash de senha para usuários de produção piloto definitivamente não é uma opção, considere Olá alternativas a seguir:
   * Crie usuários de teste no domínio de produção de hello. Certifique-se de não sincronizar nenhuma outra conta
   * Mover o ambiente de UAT tooan
2.  Se você quiser toopursue federação, vale a pena toounderstand custos de saudação associado a uma solução federada com o provedor de identidade local além Olá POC e medidas que contra Olá beneficiam que você está procurando:
    * É no caminho crítico Olá para que você tenha toodesign para alta disponibilidade
    * É um serviço local é necessário toocapacity plano
    * É um serviço local é necessário toomonitor/manter/patch

Saiba mais: [Compreendendo a identidade do Office 365 e o Azure Active Directory - Identidade Federada](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Identidade visual

Aproximar tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Ativos (imagens, logotipos, etc.); Para melhor visualização Certifique-se ativos de saudação ter Olá recomendado tamanhos. | [Adicionar identidade visual tooyour página de entrada de saudação do Active Directory do Azure](active-directory-branding-custom-signon-azure-portal.md) |
| Opcional: Se o ambiente de saudação tiver um servidor ADFS, acessar tema da web do toohello server toocustomize | [Personalização de entrada do usuário AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Experiência de logon do usuário final do tooperform de computador cliente |  |
| Opcional: Dispositivos móveis toovalidate experiência |  |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Vá tooAzure AD Portal de gerenciamento | [Portal de Gerenciamento do AD do Azure - Marca da Empresa](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Carregar ativos Olá para a página de logon da saudação (logotipo herói logotipo pequeno, rótulos, etc.). Opcionalmente, se você tiver o AD FS, alinhar Olá mesmo ativos com páginas de logon do ADFS | [Adicionar identidade visual tooyour entrar e páginas de painel de acesso da empresa: elementos personalizáveis](active-directory-add-company-branding.md) |
| Aguarde alguns minutos para Olá alterar toofully têm efeito |  |
| Faça logon com hello POC usuário credencial toohttps://myapps.microsoft.com |  |
| Confirmar Olá aparência no navegador | [Adicionar identidade visual tooyour entrar e páginas de painel de acesso da empresa](active-directory-add-company-branding.md) |
| Opcionalmente, confirme Olá aparência em outros dispositivos |  |

### <a name="considerations"></a>Considerações

Se Olá antigo aparência permanece depois da personalização Olá liberar o cache do cliente navegador hello e repita a operação de saudação.

## <a name="group-based-licensing"></a>Licenciamento baseado em grupo

Aproximar tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Todos os usuários de prova de conceito fazem parte de um grupo de segurança (nuvem ou local) | [Criar um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Folha de toolicenses vá no Portal de gerenciamento do AD do Azure | [Portal de Gerenciamento do Azure AD: Licenciamento](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Atribua o grupo de segurança de toohello Olá licenças com usuários POC. | [Atribuir licenças tooa grupo de usuários no Active Directory do Azure](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Considerações

No caso de problemas, vá muito[cenários, limitações e problemas conhecidos com o uso de grupos toomanage licenciamento no Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>Configuração de SSO Federado SaaS

Aproximar tempo tooComplete: 60 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Ambiente de saudação SaaS aplicativo disponível de teste. Neste guia, usamos o ServiceNow como um exemplo.<br/>É altamente recomendável toouse uma fricção de toominimize de instância de teste na navegação mapeamentos e qualidade de dados existente. | Vá toohttps://developer.servicenow.com/app.do#! /Home toostart processo de saudação da obtenção de uma instância de teste |
| Console de gerenciamento do administrador acesso toohello ServiceNow | [Tutorial: Integração do Active Directory do Azure com o ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Conjunto de usuários tooassign Olá aplicativo de destino. Recomenda-se um grupo de segurança que contém os usuários de PoC hello. <br/>Se a criação do grupo de saudação não for viável, atribuir usuários Olá toodirectly toohello aplicativo hello PoC | [Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Compartilhar os atores tooall tutorial de saudação do Microsoft Documentation  | [Tutorial: Integração do Active Directory do Azure com o ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Defina uma reunião de trabalho e execute as etapas de tutorial Olá com cada ator. | [Tutorial: Integração do Active Directory do Azure com o ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Atribua Olá aplicativo toohello grupo identificado na Olá pré-requisitos. Se Olá POC tenha acesso condicional no escopo de hello, poderá revisá que mais tarde e adicionar MFA e semelhante. <br/>Observe que isso será iniciada Olá processo de provisionamento (se configurado) |  [Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Criar um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Usar o AD do Azure management Portal tooadd ServiceNow aplicativo da Galeria| [Portal de Gerenciamento do Azure AD: Aplicativos Empresariais](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[O que há de novo no gerenciamento de Aplicativos Empresariais no Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| Na folha "Logon único" do Aplicativo ServiceNow, habilite "Logon único baseado em SAML" |  |
| Preencha os campos "URL de Entrada" e "Identificador" com a URL de ServiceNow<br/>Caixa de saudação seleção muito "Ativar novo certificado"<br/>e em Salvar configurações |  |
| Abrir folha "Configurar ServiceNow" na parte inferior de saudação do hello painel tooview personalizado instruções para você tooconfigure ServiceNow |  |
| Siga as instruções tooconfigure ServiceNow |  |
| Na folha "Provisionamento" do Aplicativo ServiceNow habilite o provisionamento "Automático" | [Gerenciar a conta de usuário de provisionamento para aplicativos da empresa no novo portal do Azure de saudação](active-directory-enterprise-apps-manage-provisioning.md) |
| Aguarde alguns minutos enquanto o provisionamento é concluído.  Em Olá enquanto isso, você pode verificar Olá provisionamento relatórios |  |
| Faça logon em toohttps://myapps.microsoft.com/ como um usuário de teste que tem acesso | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |
| Clique no bloco de saudação do aplicativo hello que acabou de ser criado. Confirmar o acesso |  |
| Opcionalmente, você pode verificar relatórios de uso do aplicativo hello. Observe que há alguma latência, portanto, você precisa toowait algum tráfego de saudação toosee tempo nos relatórios de saudação. | [Relatórios de atividade de entrada no portal do Azure Active Directory Olá: uso de aplicativos gerenciados](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Políticas de retenção de relatório do Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considerações

1. Acima [Tutorial](active-directory-saas-servicenow-tutorial.md) refere-se a experiência de gerenciamento tooold AD do Azure. Mas a prova de conceito baseia-se em experiência de [Início Rápido ](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away).
2. Se o aplicativo de destino hello não está presente na Galeria de saudação, você pode usar "Traga seu próprio aplicativo". Saiba mais em: [O que há de novo no gerenciamento de Aplicativos Empresariais no Azure Active Directory: Adicionar aplicativos personalizados de um local](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>Configuração do SSO de senha de SaaS

Aproximar tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Ambiente de teste para aplicativos SaaS. Um exemplo de SSO de senha é HipChat e o Twitter. Para qualquer outro aplicativo, você precisa Olá a URL exata da página de saudação com o formulário de entrada html. | [Twitter no Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat no Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Contas para aplicativos de saudação de teste. | [Inscrever-se para Twitter](https://twitter.com/signup?lang=en)<br/>[Inscreva-se para avaliação gratuita: HipChat](https://www.hipchat.com/sign_up) |
| Conjunto de usuários tooassign Olá aplicativo de destino. É recomendável uma segurança grupo contido Olá usuários. | [Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure](active-directory-coreapps-assign-user-azure-portal.md) |
| Olá administrador local acesso tooa computador toodeploy extensão do painel de acesso para o Internet Explorer, Chrome ou Firefox | [Extensão do Painel de Acesso do IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão do Painel de Acesso do Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão do Painel de Acesso do Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Instalar a extensão de navegador Olá | [Extensão do Painel de Acesso do IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão do Painel de Acesso do Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão do Painel de Acesso do Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurar um Aplicativo da Galeria | [Novidades no gerenciamento de aplicativos de empresa no Active Directory do Azure: Galeria de aplicativos novos e aprimorados Olá](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurar SSO de Senha | [Gerenciar logon único para aplicativos da empresa no novo portal do Azure de saudação: com base em senha de logon](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Atribuir Olá aplicativo toohello grupo identificado na Olá pré-requisitos | [Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure](active-directory-coreapps-assign-user-azure-portal.md) |
| Faça logon em toohttps://myapps.microsoft.com/ como um usuário de teste que tem acesso |  |
| Clique no bloco de saudação do aplicativo hello que acabou de ser criado. | [O que é o painel de acesso de saudação?: SSO baseado em senha sem provisionamento de identidade](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Forneça credenciais de aplicativo hello | [O que é o painel de acesso de saudação?: SSO baseado em senha sem provisionamento de identidade](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Feche o navegador hello e logon Olá repetição. Agora o usuário de saudação deve aparecer o aplicativo de toohello de acesso contínuo. |  |
| Opcionalmente, você pode verificar relatórios de uso do aplicativo hello. Observe que há alguma latência, portanto, você precisa toowait algum tráfego de saudação toosee tempo nos relatórios de saudação. | [Relatórios de atividade de entrada no portal do Azure Active Directory Olá: uso de aplicativos gerenciados](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Políticas de retenção de relatório do Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considerações

Se o aplicativo de destino hello não está presente na Galeria de saudação, você pode usar "Traga seu próprio aplicativo". Saiba mais em: [O que há de novo no gerenciamento de Aplicativos Empresariais no Azure Active Directory: Adicionar aplicativos personalizados de um local](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Lembre-Olá mente requisitos a seguir:
   * O aplicativo deve ter uma URL de logon conhecida
   * página de entrada Hello deve conter um formulário HTML com um mais campos de texto que extensões de navegador Olá podem preencher automaticamente. Em Olá mínimo, ela deve conter o nome de usuário e senha.

## <a name="saas-shared-accounts-configuration"></a>Configuração de Contas Compartilhadas SaaS

Aproximar tempo tooComplete: 30 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Olá a lista de aplicativos de destino e Olá URLS de entrada exato antecipadamente. Por exemplo, você pode usar o Twitter. | [Twitter no Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Inscrever-se para Twitter](https://twitter.com/signup?lang=en) |
| Credencial compartilhada para esse aplicativo SaaS. | [Compartilhando contas usando o Azure AD](active-directory-sharing-accounts.md)<br/>[Transferência de senha automatizada do Azure AD para Facebook, Twitter e LinkedIn agora na versão prévia! - Blog de segurança e mobilidade corporativa] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/ ) |
| As credenciais para pelo menos dois membros da equipe que irá acessar Olá a mesma conta. Eles devem ser parte de um grupo de segurança. | [Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure](active-directory-coreapps-assign-user-azure-portal.md) |
| Olá administrador local acesso tooa computador toodeploy extensão do painel de acesso para o Internet Explorer, Chrome ou Firefox | [Extensão do Painel de Acesso do IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão do Painel de Acesso do Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão do Painel de Acesso do Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Instalar a extensão de navegador Olá | [Extensão do Painel de Acesso do IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão do Painel de Acesso do Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão do Painel de Acesso do Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurar um Aplicativo da Galeria | [Novidades no gerenciamento de aplicativos de empresa no Active Directory do Azure: Galeria de aplicativos novos e aprimorados Olá](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurar SSO de Senha | [Gerenciar logon único para aplicativos da empresa no novo portal do Azure de saudação: com base em senha de logon](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Atribuir Olá aplicativo toohello grupo identificado na Olá pré-requisitos ao atribuir credenciais | [Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure](active-directory-coreapps-assign-user-azure-portal.md) |
| Faça logon como usuários diferentes que o aplicativo acesso como Olá **conta mesmo compartilhado.**  |  |
| Opcionalmente, você pode verificar relatórios de uso do aplicativo hello. Observe que há alguma latência, portanto, você precisa toowait algum tráfego de saudação toosee tempo nos relatórios de saudação. | [Relatórios de atividade de entrada no portal do Azure Active Directory Olá: uso de aplicativos gerenciados](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Políticas de retenção de relatório do Azure Active Directory](active-directory-reporting-retention.md) |


### <a name="considerations"></a>Considerações

Se o aplicativo de destino hello não está presente na Galeria de saudação, você pode usar "Traga seu próprio aplicativo". Saiba mais em: [O que há de novo no gerenciamento de Aplicativos Empresariais no Azure Active Directory: Adicionar aplicativos personalizados de um local](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Lembre-Olá mente requisitos a seguir:
   * O aplicativo deve ter uma URL de logon conhecida
   * página de entrada Hello deve conter um formulário HTML com um mais campos de texto que extensões de navegador Olá podem preencher automaticamente. Em Olá mínimo, ela deve conter o nome de usuário e senha.

## <a name="app-proxy-configuration"></a>Configuração de Proxy de Aplicativo

Aproximar tempo tooComplete: 20 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Uma assinatura premium ou básica do Microsoft Azure AD e um diretório do Azure AD do qual você seja administrador global | [Edições do Active Directory do Azure](active-directory-editions.md) |
| Um aplicativo web hospedado no local que você gostaria que tooconfigure para acesso remoto |  |
| Um servidor que executa o Windows Server 2012 R2 ou Windows 8.1 ou posterior, no qual você pode instalar Olá conector de Proxy de aplicativo | [Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md) |
| Se houver um firewall no caminho de saudação, certifique-se de que ele está aberto para que Olá que conector pode tornar HTTPS (TCP) solicita toohello Proxy de aplicativo | [Habilitar Proxy de aplicativo no portal do Azure de saudação: pré-requisitos do Proxy de aplicativo](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Se sua organização usa o proxy de servidores tooconnect toohello internet, execute uma olhada Olá blog post trabalhar com servidores de proxy local existente para obter detalhes sobre como tooconfigure-los | [Trabalhar com servidores proxy locais existentes](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Instalar um conector no servidor de saudação | [Habilitar Proxy de aplicativo no portal do Azure de saudação: instalar e registrar Olá conector](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Publicar aplicativo do hello local no AD do Azure como um aplicativo de Proxy de aplicativo | [Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure](application-proxy-publish-azure-portal.md) |
| Atribuir usuários de teste | [Publicar aplicativos usando o Proxy de Aplicativo do Azure AD: Adicionar um usuário de teste](application-proxy-publish-azure-portal.md#add-a-test-user) |
| Opcionalmente, configure uma experiência de logon único para seus usuários | [Fornecer logon único com o Proxy de Aplicativo do Azure AD](application-proxy-sso-azure-portal.md) |
| Aplicativo de teste ao entrar no portal de tooMyApps como atribuído a usuário | https://myapps.microsoft.com |

### <a name="considerations"></a>Considerações

1. Enquanto é recomendável colocar o conector de saudação em sua rede corporativa, há casos em que você verá um melhor desempenho, colocando-os em nuvem hello. Saiba mais em: [Considerações de topologia de rede ao usar o Proxy de Aplicativo do Azure Active Directory](application-proxy-network-topology-considerations.md)
2. Para obter mais detalhes de segurança e como isso fornece uma solução de acesso remoto particularmente segura, mantendo apenas conexões de saída, consulte: [Considerações de segurança para acessar aplicativos remotamente usando o Proxy de Aplicativo do Azure AD](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>Configuração do Conector LDAP Genérico

Aproximar tempo tooComplete: 60 minutos

> [!IMPORTANT]
> Esta é uma configuração avançada que exige alguma familiaridade com o FIM/MIM. Se usada em produção, aconselhamos consulgar as perguntas sobre essa configuração através do [Suporte Premier](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Azure AD Connect instalado e configurado | Bloco de construção: [Sincronização de Diretórios - PHS (sincronização de hash de senha)](#directory-synchronization--password-hash-sync-phs--new-installation) |
| Atendendo aos requisitos de instância ADLDS | [Referência técnica de conector LDAP genérica: Visão geral da saudação conector de LDAP genérico](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Lista de cargas de trabalho que os usuários estão usando e atributos associados a essas cargas de trabalho | [Sincronização do Azure AD Connect: atributos sincronizados tooAzure do Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Adicionar Conector LDAP Genérica | [Referência Técnica do Conector LDAP Genérica: Criar um novo Conector](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Criar perfis de execução para o conector criado (importação completa, importação Delta, sincronização completa, sincronização Delta, exportação) | [Criar um Perfil de Execução de Agente de Gerenciamento](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [Usando conectores com hello Azure AD Connect sincronização Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Execute o perfil de importação completa e verifique se há objetos no espaço conector | [Pesquisar um Objeto do Espaço Conector](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[Usando conectores com hello sincronização Service Manager do Azure AD Connect: pesquisa de espaço do conector](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Criar regras de sincronização para que os objetos no Metaverso tenham atributos necessários para cargas de trabalho | [Sincronização do Azure AD Connect: práticas recomendadas para alterar a configuração padrão de saudação: alterar as regras de tooSynchronization](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Sincronização do Azure AD Connect: noções básicas sobre expressões de provisionamento declarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect Sync: Noções básicas sobre Expressões de Provisionamento Declarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Inicie o ciclo de sincronização completa | [Sincronização do Azure AD Connect: Agendador: Inicie o Agendador de saudação](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| Em caso de problemas execute a solução de problemas | [Solucionar problemas de um objeto que não está sincronizando tooAzure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Verifique se, usuário LDAP pode entrar e acessar o aplicativo hello | https://myapps.microsoft.com |

### <a name="considerations"></a>Considerações

> [!IMPORTANT]
> Esta é uma configuração avançada que exige alguma familiaridade com o FIM/MIM. Se usada em produção, aconselhamos consulgar as perguntas sobre essa configuração através do [Suporte Premier](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Grupos - Propriedade Delegada

Aproximar tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Aplicativo de SaaS (SSO federado ou SSO de senha) foi já configurado | Bloco de construção: [Configuração de SSO Federado SaaS](#saas-federated-sso-configuration) |
| Grupo de nuvem que recebe acesso toohello aplicativo # 1 é identificado | Bloco de construção: [Configuração de SSO Federado SaaS](#saas-federated-sso-configuration) <br/>[Criar um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| As credenciais para o proprietário do grupo Olá estão disponíveis | [Gerenciar acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md) |
| As credenciais para aplicativos trabalho Olá acessando informações Olá foi identificado | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Identificar Olá grupo que tenha sido concedido acesso toohello aplicativo e configure o proprietário de saudação de um determinado grupo| [Gerenciar configurações de saudação para um grupo no Active Directory do Azure](active-directory-groups-settings-azure-portal.md) |
| Faça logon como proprietário do grupo hello, consulte a associação de grupo Olá no guia de grupos do painel de acesso | [Página de Gerenciamento de Grupos do Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Adicionar operador de informações de saudação desejado tootest |  |
| Faça logon como operador de informações Olá, confirme a saudação bloco está disponível | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Considerações

Se o aplicativo hello tiver habilitado o provisionamento, talvez seja necessário toowait alguns minutos para Olá provisionamento toocomplete antes de acessar o aplicativo hello como operador de informações de saudação.

## <a name="saas-and-identity-lifecycle"></a>Ciclo de vida de identidade e SaaS

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Aplicativo de SaaS (SSO federado ou SSO de senha) foi já configurado | Bloco de construção: [Configuração de SSO Federado SaaS](#saas-federated-sso-configuration) |
| Grupo de nuvem que recebe acesso toohello aplicativo # 1 é identificado | Bloco de construção: [Configuração de SSO Federado SaaS](#saas-federated-sso-configuration) <br/>[Criar um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| As credenciais para aplicativos trabalho Olá acessando informações Olá foi identificado | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Remover usuário Olá Olá grupo Olá aplicativo recebe muito| [Gerenciar associação de grupo de usuários em seu locatário do Azure Active Directory](active-directory-groups-members-azure-portal.md) |
| Aguarde alguns minutos para desprovisionamento | [Provisionamento de Usuário de Aplicativo SaaS Automatizado do Azure AD: Como fazer o trabalho de provisionamento automatizado?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| Em uma sessão separada do navegador, faça logon como o portal de aplicativos do hello informações trabalho toomy e confirmar que está ausente | http://myapps.microsoft.com |


### <a name="considerations"></a>Considerações

Extrapole Olá PoC cenário tooleavers e/ou em cenários de licença. Se o usuário Olá obtém desabilitado no AD local ou removido, não é mais uma maneira toolog em toohello aplicativo SaaS.

## <a name="self-service-access-tooapplication-management"></a>Autoatendimento acesso ao serviço tooApplication gerenciamento

Aproximar tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identificar os usuários POC que solicitarem acesso toohello aplicativos, como parte do grupo de segurança de saudação | Bloco de construção: [Configuração de SSO Federado SaaS](#saas-federated-sso-configuration) |
| Aplicativo de Destino Implantado | Bloco de construção: [Configuração de SSO Federado SaaS](#saas-federated-sso-configuration) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Vá tooEnterprise folha de aplicativos no Portal de gerenciamento do AD do Azure | [Portal de Gerenciamento do Azure AD: Aplicativos Empresariais](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Configurar o Aplicativo de Pré-requisitos com serviço de autoatendimento | [O que há de novo no gerenciamento de Aplicativos Empresariais no Azure Active Directory: Configurar o acesso ao aplicativo de autoatendimento](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Faça logon como o portal de aplicativos do hello informações trabalho toomy | http://myapps.microsoft.com |
| Observe "+ Adicionar aplicativo" botão em operações de página hello. Usá-lo tooget acesso toohello aplicativo |  |

### <a name="considerations"></a>Considerações

aplicativos de saudação escolhidos podem ter requisitos, o provisionamento para que ir imediatamente toohello aplicativo pode fazer com que alguns erros. Se o aplicativo hello escolhido dá suporte ao provisionamento com o azure ad e é configurado, você pode usar isso como um oportunidade tooshow Olá todo fluxo trabalhando tooend final. Consulte o bloco de construção de saudação para [SaaS federado SSO configuração](#saas-federated-sso-configuration) para obter mais recomendações

## <a name="self-service-password-reset"></a>Redefinição de senha por autoatendimento

Aproximar tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Tipos de atividades de gerenciamento de senha de autoatendimento no seu locatáro. | [Redefinição de senhas do Azure Active Directory para administradores de TI](active-directory-passwords.md) |
| Ativar senha toomanage de write-back de senhas do local. Observe que isso exige versões do Azure AD Connect | [Pré-requisitos de Write-back de Senha](active-directory-passwords-writeback.md) |
| Identifique os usuários de PoC de saudação que usará essa funcionalidade e verifique se que eles são membros de um grupo de segurança. usuários Olá devem ser o recurso de saudação do não-administradores toofully showcase | [Personalizar: Gerenciamento de senha do Azure AD: restringir o acesso toopassword redefinição](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Navegue tooAzure AD Portal de gerenciamento: redefinição de senha | [Portal de Gerenciamento do Azure AD: Redefinição de senha](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Determine a política de redefinição de senha de saudação. Para fins POC, você pode usar chamada telefônica e p e r. É recomendável tooenable registro toobe necessário em log no painel de tooaccess |  |
| Faça logoff e logon como um operador de informações |  |
| Fornecer dados de redefinição de senha de autoatendimento de saudação conforme configurado por etapa 2 | http://aka.ms/ssprsetup |
| Navegador de saudação fechar |  |
| Iniciar processo de logon hello como operador de informações de saudação usado na etapa 4 |  |
| Redefinir senha Olá | [Atualizar sua própria senha: Redefinir a minha senha](active-directory-passwords-update-your-own-password.md) |
| Tente fazer logon com sua nova senha tooAzure AD, assim como os recursos de tooon local |  |

### <a name="considerations"></a>Considerações

1. Se atualizar hello Azure AD Connect será toocause fricção, considere usá-lo em relação a contas de nuvem ou torná-lo uma demonstração em um ambiente separado
2. Olá tem uma política diferente e usando Olá administrador senha da conta tooreset Olá pode taint Olá PoC e causar confusão. Verifique se que você usar um operações de redefinição de saudação do usuário regular conta tootest


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Autenticação Multifator do Azure com Chamadas Telefônicas

Aproximar tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identificar os usuários de prova de conceito que usam MFA  |  |
| Telefone com bom sinal para o desafio MFA  | [O que é a Autenticação Multifator do Azure?](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Navegue muito folha "Usuários e grupos" no Portal de gerenciamento do AD do Azure | [Portal de Gerenciamento do Azure AD: Usuários e grupos](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Selecione a folha "Todos os usuários" |  |
| Na parte superior da saudação barra botão de "Multi-Factor Authentication" escolher | URL Direta para o portal MFA do Azure: https://aka.ms/mfaportal |
| Em configurações de "Usuário" hello selecione Olá PoC usuários e habilitá-las para MFA | [Estados do usuário na Autenticação Multifator do Azure](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Faça logon como usuário de PoC hello e passo a passo do processo de verificação Olá  |  |

### <a name="considerations"></a>Considerações

1. Olá PoC etapas para este bloco de construção definir explicitamente o MFA para um usuário em todos os logons. Há outras ferramentas, como Acesso Condicional e Proteção de Identidade que envolvem MFA em outros cenários de destino. Isso será algo tooconsider ao mover de POC tooproduction.
2. etapas de PoC Olá neste bloco de construção são explicitamente usando chamadas telefônicas como Olá método MFA para expedience. Como fazer a transição do VDC tooproduction, recomendamos o uso de aplicativos como Olá [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) como o segundo fator sempre que possível.
Saiba mais em: [Publicação Especial DRAFT NIST 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>Acesso Condicional com MFA para Aplicativos SaaS

Aproximar tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identifica PoC usuários tootarget Olá diretiva. Esses usuários devem estar em uma política de acesso condicional segurança grupo tooscope Olá | [Configuração de SSO federado SaaS](#saas-federated-sso-configuration) |
| O aplicativo de SaaS foi já configurado |  |
| Os usuários de PoC já estão atribuídos toohello aplicativo |  |
| Usuário POC toohello credenciais estão disponíveis |  |
| Usuário de prova de conceito está registrado para MFA. Usando um telefone com bom sinal | http://aka.ms/ssprsetup |
| Dispositivo na rede interna hello. Endereço IP configurado no intervalo de endereço interno Olá | Localize do endereço IP em: https://www.bing.com/search?q=what%27s+my+ip |
| Dispositivo na rede externa de saudação (pode ser um telefone usando rede móvel da operadora Olá) |  |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Vá tooAzure AD Portal de gerenciamento: folha de acesso condicional | [Portal de Gerenciamento do Azure AD: Folha de acesso condicional](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Criar política de Acesso Condicional:<br/>-Usuários de PoC de destino em "Usuários e grupos"<br/>-Aplicativo de PoC de destino em "Aplicativos de nuvem"<br/>-Todos os locais de destino exceto os confiáveis em "Condições"-> "Locais" **Observação:** IPs confiáveis são configurados no [Portal MFA](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)<br/>- Exigir autenticação multifator em "Conceder" | [Introdução ao acesso condicional no Azure Active Directory: Etapas de configuração de política](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Aplicativo de acesso de dentro de rede corporativa | [Introdução ao acesso condicional no Active Directory do Azure: teste a política de saudação](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Aplicativo de acesso de rede pública | [Introdução ao acesso condicional no Active Directory do Azure: teste a política de saudação](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Considerações

Se você estiver usando a federação, você pode usar Olá Olá de toocommunicate de provedor de identidade (IdP) local dentro/fora o estado da rede corporativa com declarações. Você pode usar essa técnica sem ter toomanage Olá lista de endereços IP que podem ser complexos tooassess e gerenciar em grandes organizações. Em que a instalação, você precisa de conta para o cenário de "rede móvel" hello (um usuário e de registro de rede interna hello, enquanto conectados comutadores locais como uma cafeteria) e certifique-se de que compreender as implicações de saudação. Saiba mais em: [Protegendo os recursos da nuvem com Autenticação Multifator do Azure e AD FS: IPs confiáveis para usuários federados](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>PIM (Privileged Identity Management)

Aproximar tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identificar Olá administrador global que farão parte da saudação POC para o PIM | [Começar a usar o Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Identificar Olá administrador global que se tornarão Olá administrador de segurança | [Começar a usar o Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Funções administrativas diferentes no PIM do Azure Active Directory](active-directory-privileged-identity-management-roles.md) |
| Opcional: Confirmar se os administradores globais Olá tem email tooexercise notificações de email no Gerenciador de acesso | [O que é o Azure AD Privileged Identity Management?: definir configurações de ativação de função hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Toohttps://portal.azure.com logon como um administrador global (GA) e a folha PIM Olá inicialização. Olá Administrador Global que executa essa etapa é propagado como administrador de segurança de saudação.  Vamos chamar isso de ator GA1 | [Usando o Assistente de segurança Olá no Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Identificar Olá administrador global e movê-los de tooeligible permanente. Isso deve ser um administrador separada da saudação usado na etapa 1 para maior clareza. Vamos chamar isso de ator GA2 | [Azure AD Privileged Identity Management: Como tooadd ou remover uma função de usuário](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[O que é o Azure AD Privileged Identity Management?: definir configurações de ativação de função hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Agora, faça logon como GA2 toohttps://portal.azure.com e tente alterar "Configurações de usuário". Observe que algumas opções estão esmaecidas. | |
| Em uma nova guia em Olá mesma sessão como a etapa 3, navegue toohttps://portal.azure.com agora e adicionar Olá PIM folha toohello painel. | [Como tooactivate ou desativar funções no Azure AD Privileged Identity Management: adicionar o aplicativo do hello Privileged Identity Management](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Função de Administrador Global de toohello de ativação de solicitação | [Como tooactivate ou desativar funções no Azure AD Privileged Identity Management: ativar uma função](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Observe que se GA2 nunca se inscreveu para MFA, o registro para o Azure MFA será necessário |  |
| Volte à guia de toohello original na etapa 3 e clique botão de atualização de saudação no navegador de saudação. Observe que agora você tem acesso toochange "Configurações de usuário" | |
| Opcionalmente, se os administradores globais têm email ativado, você pode verificar GA1 e da GA2 caixa de entrada e ver a notificação de saudação da função hello está sendo ativada |  |
| 8 Verifique o histórico de auditoria hello e observe a elevação de saudação do hello relatório tooconfirm de GA2 é mostrada. | [O que é o Azure AD Privileged Identity Management?: Examinar a atividade da funçãol](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Considerações

Esse recurso faz parte do Azure AD Premium P2 e/ou EMS E5

## <a name="discovering-risk-events"></a>Descoberta de Eventos de Risco

Aproximar tempo tooComplete: 20 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Dispositivo com Navegador Tor baixado e instalado | [Baixe o Navegador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Logon de saudação do acesso tooPOC usuário toodo | [Guia estratégico do Azure Active Directory Identity Protection](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Abra o navegador Tor | [Baixe o Navegador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Faça logon no toohttps://myapps.microsoft.com com hello conta de usuário do VDC | [Guia estratégico do Azure Active Directory Identity Protection: Simulação de Eventos de Risco](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Aguarde de 5 a 7 minutos |  |
| Faça logon como um administrador global toohttps://portal.azure.com e abra a folha de proteção de identidade Olá | https://aka.ms/aadipgetstarted |
| Folha de eventos de risco Olá aberto. Você deve ver uma entrada em "Entradas de endereços IP anônimos"  | [Guia estratégico do Azure Active Directory Identity Protection: Simulação de Eventos de Risco](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Considerações

Esse recurso faz parte do Azure AD Premium P2 e/ou EMS E5

## <a name="deploying-sign-in-risk-policies"></a>Implantação de políticas de risco de logon

Aproximar tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Dispositivo com Navegador Tor baixado e instalado | [Baixe o Navegador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Acesso um log de saudação POC usuário toodo no teste |  |
| O usuário de POC está registrado com MFA. Certifique-se de que toouse um telefone com boa recepção | Bloco de Construção: [Autenticação Multifator do Azure com Chamadas Telefônicas](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Faça logon como um administrador global toohttps://portal.azure.com e abra a folha de proteção de identidade Olá | https://aka.ms/aadipgetstarted |
| Habilite uma política de risco de entrada conforme a seguir:<br/>-Atribuído a: usuário de POC<br/>-Condições: Risco de entrada médio ou superior (entrada de local anônimo é considerada como um nível de risco médio)<br/>-Controles: Exigir MFA | [Guia estratégico do Azure Active Directory Identity Protection: Risco de entrada](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Abra o navegador Tor | [Baixe o Navegador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Faça logon no toohttps://myapps.microsoft.com com hello PoC conta de usuário |  |
| Saudação de aviso desafio MFA | [Experiências de entrada com o Azure AD Identity Protection: Recuperação de entrada de risco](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Considerações

Esse recurso faz parte do Azure AD Premium P2 e/ou EMS E5. toolearn mais sobre eventos de risco, visite: [eventos de risco do Active Directory do Azure](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Configurando autenticação baseada em certificado

Aproximar tempo toocomplete: 20 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Dispositivo com certificado do usuário provisionado (Windows, iOS ou Android) da Enterprise PKI | [Implantar Certificados do Usuário](https://msdn.microsoft.com/library/cc770857.aspx) |
| Domínio do Azure AD federado com ADFS | [Azure AD Connect e federação](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Visão geral dos Serviços de Certificados do Active Directory](https://technet.microsoft.com/library/hh831740.aspx)|
| Para dispositivos iOS tem o aplicativo Microsoft Authenticator instalado | [Introdução ao aplicativo do Microsoft Authenticator Olá](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Etapas

| Etapa | Recursos |
| --- | --- |
| Habilitar "Autenticação de Certificado" no ADFS | [Configurar políticas de autenticação: autenticação primária tooconfigure globalmente no Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Opcional: Habilitar a Autenticação de Certificado no Azure AD para clientes do Exchange Active Sync | [Introdução à autenticação baseada em certificado no Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Navegue tooAccess painel e autenticar usando um certificado de usuário | https://myapps.microsoft.com |

### <a name="considerations"></a>Considerações

toolearn mais sobre advertências dessa implantação, visite: [ADFS: autenticação de certificado com o Azure AD & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> A posse do certificado do usuário deve ser protegida. Por meio de gerenciamento de dispositivos ou por PIN, no caso de cartões inteligentes.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
