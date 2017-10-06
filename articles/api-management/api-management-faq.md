---
title: Perguntas frequentes sobre o gerenciamento de API de aaaAzure | Microsoft Docs
description: "Aprenda a saudação responde perguntas toocommon, padrões e práticas recomendadas para gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Perguntas frequentes sobre Gerenciamento de API do Azure
Obter Olá respostas toocommon perguntas, padrões e práticas recomendadas para gerenciamento de API do Azure.

## <a name="contact-us"></a>Fale conosco
* [Como fazer uma pergunta de equipe de gerenciamento de API do Microsoft Azure Olá?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Perguntas frequentes
* [O que significa quando um recurso está em visualização?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Como proteger a conexão de saudação entre o gateway de gerenciamento de API hello e meus serviços de back-end?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Como copiar o gerenciamento de API serviço tooa nova instância?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [Posso gerenciar minha instância de Gerenciamento de API por meio de programação?](#can-i-manage-my-api-management-instance-programmatically)
* [Como adicionar um grupo de administradores de usuário toohello?](#how-do-i-add-a-user-to-the-administrators-group)
* [Por que é política Olá que desejo tooadd não está disponível no editor de política Olá?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Como usar o controle de versão de API no Gerenciamento de API?](#how-do-i-use-api-versioning-in-api-management)
* [Como configurar vários ambientes em uma única API?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [Pode usar o SOAP com Gerenciamento de API?](#can-i-use-soap-with-api-management)
* [É a constante de endereço IP de gateway do Olá gerenciamento de API? Posso usá-lo nas regras de firewall?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Posso configurar um servidor de autorização OAUth 2.0 com segurança ADFS?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [O método de roteamento de gerenciamento de API usar em localizações geográficas de toomultiple implantações?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [É possível usar um modelo de Gerenciador de recursos do Azure toocreate uma instância do serviço de gerenciamento de API?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Posso usar um certificado SSL autoassinado para um back-end?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Por que recebo uma falha de autenticação quando tento tooclone um repositório GIT?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [O Gerenciamento de API funciona com o Azure ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [Por que exigimos uma sub-rede dedicada em Resource Manager tipo VNETs quando o Gerenciamento de API é implantado nelas?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Qual é o tamanho de sub-rede mínimo de saudação necessário ao implantar a API de gerenciamento em uma rede virtual?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Pode mover um serviço de gerenciamento de API de um tooanother de assinatura?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Há restrições ou problemas conhecidos com a importação da minha API?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Como fazer uma pergunta de equipe de gerenciamento de API do Microsoft Azure Olá?
Você pode em contato conosco utilizando uma das seguintes opções:

* Poste suas perguntas em nossos [Fórum do MSDN de Gerenciamento de API](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Enviar um email muito<mailto:apimgmt@microsoft.com>.
* Envie uma solicitação de recurso no hello [Fórum de comentários do Azure](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>O que significa quando um recurso está em visualização?
Quando um recurso está em visualização, isso significa que podemos está empenhada comentários sobre como o recurso de saudação está funcionando para você. Um recurso de visualização é funcionalmente completo, mas é possível que será feita uma quebra de alteração em comentários de toocustomer de resposta. É recomendável que você não dependa de um recurso que está na visualização em seu ambiente de produção. Se você tiver algum comentário sobre os recursos de visualização, informe-por meio de uma das opções de contato de saudação em [como posso fazer equipe de gerenciamento de API do Microsoft Azure Olá uma pergunta?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Como proteger a conexão de saudação entre o gateway de gerenciamento de API hello e meus serviços de back-end?
Você tem várias conexão de saudação toosecure opções entre o gateway de gerenciamento de API hello e seus serviços de back-end. Você pode:

* Use a autenticação básica HTTP. Para saber mais, confira [Definir configurações de API](api-management-howto-create-apis.md#configure-api-settings).
* Usar autenticação mútua de SSL, conforme descrito em [como os serviços de back-end toosecure usando a autenticação de certificado de cliente no gerenciamento de API do Azure](api-management-howto-mutual-certificates.md).
* Use a lista branca de IPs em seu serviço de back-end. Se você tiver uma instância de gerenciamento de API da camada Standard ou Premium, o endereço IP de saudação do gateway de saudação permanece constante. Você pode definir sua lista branca tooallow esse endereço IP. Você pode obter o endereço IP de saudação da sua instância de gerenciamento de API em Olá painel no hello portal do Azure.
* Conecte-se a instância de gerenciamento de API tooan rede Virtual do Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>Como copiar o gerenciamento de API serviço tooa nova instância?
Se você quiser toocopy uma gerenciamento de API tooa nova instância, você tem várias opções. Você pode:

* Use Olá backup e restaurar a função no gerenciamento de API. Para obter mais informações, consulte [como tooimplement a recuperação de desastres usando serviço de backup e restauração no gerenciamento de API do Azure](api-management-howto-disaster-recovery-backup-restore.md).
* Criar seu próprio backup e restaurar o recurso usando Olá [API de REST de gerenciamento de API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Usar toosave da API REST de saudação e restauração de entidades de saudação da instância de serviço Olá que você deseja.
* Baixar a configuração do serviço hello usando o Git e, em seguida, carregá-lo tooa nova instância. Para obter mais informações, consulte [como toosave e configurar a configuração do serviço de gerenciamento de API usando o Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>Posso gerenciar minha instância de Gerenciamento de API por meio de programação?
Sim, você pode gerenciar o Gerenciamento de API de forma programática, usando:

* Olá [API de REST de gerenciamento de API](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Olá [SDK biblioteca de gerenciamento de serviço do Microsoft Azure ApiManagement](http://aka.ms/apimsdk).
* Olá [implantação de serviço](https://msdn.microsoft.com/library/mt619282.aspx) e [gerenciamento de serviço](https://msdn.microsoft.com/library/mt613507.aspx) cmdlets do PowerShell.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Como adicionar um grupo de administradores de usuário toohello?
Aqui está como você pode adicionar um grupo de administradores de toohello de usuário:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Vá toohello grupo de recursos com instância de gerenciamento de API Olá deseja tooupdate.
3. No gerenciamento de API, atribuir Olá **Colaborador de gerenciamento de Api** usuário de toohello de função.

Agora Olá recém-adicionado colaborador pode usar o Azure PowerShell [cmdlets](https://msdn.microsoft.com/library/mt613507.aspx). Aqui está como toosign no como administrador:

1. Saudação de uso `Login-AzureRmAccount` toosign cmdlet no.
2. Definir Olá contexto toohello assinatura com o serviço de saudação usando `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Obter uma única URL de logon usando `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Use o portal de administração do hello URL tooaccess hello.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Por que é política Olá que desejo tooadd não está disponível no editor de política Olá?
Se a política de saudação que você deseja tooadd aparece esmaecido ou sombreados no editor de diretiva de hello, certifique-se que você está no escopo correto de saudação para política de saudação. Cada declaração de política foi criada para você toouse nas seções de política e escopos específicos. seções de política tooreview hello e escopos de uma política, consulte o uso da diretiva de saudação seção [políticas de gerenciamento de API](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Como usar o controle de versão de API no Gerenciamento de API?
Você tem controle de versão API toouse de algumas opções no gerenciamento de API:

* No gerenciamento de API, você pode configurar versões diferentes de toorepresent APIs. Por exemplo, você pode ter duas APIs diferentes, MyAPIv1 e MyAPIv2. Um desenvolvedor pode escolher a versão Olá Olá desenvolvedor quer toouse.
* Você também pode configurar sua API com uma URL de serviço que não inclua um segmento de versão, por exemplo, https://my.api. Em seguida, configure um segmento de versão no modelo [Regravar URL](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) de cada operação . Por exemplo, você pode ter uma operação com um [modelo de URL](api-management-howto-add-operations.md#url-template) chamado /resource e um modelo de [URL de regravação](api-management-howto-add-operations.md#rewrite-url-template) chamado /v1/Resource. Você pode alterar o valor de segmento de versão Olá separadamente para cada operação.
* Se você gostaria que tookeep um segmento de versão "padrão" na URL de serviço de saudação da API, em operações selecionadas, definir uma política que usa Olá [Configurar serviço de back-end](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) caminho da solicitação de back-end política toochange hello.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Como configurar vários ambientes em uma única API?
tooset vários ambientes, por exemplo, um ambiente de teste e um ambiente de produção, em uma única API, você tem duas opções. Você pode:

* APIs de host diferentes em Olá mesmo locatário.
* Host Olá as mesmas APIs em locatários diferentes.

### <a name="can-i-use-soap-with-api-management"></a>Pode usar SOAP com Gerenciamento de API?
O suporte a [Passagem SOAP](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) agora está disponível. Os administradores podem importar Olá WSDL do seu serviço de SOAP e gerenciamento de API do Azure criará um front-end SOAP. Documentação do portal de desenvolvedor, console de teste, políticas e análise estão disponíveis para serviços SOAP.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>É a constante de endereço IP de gateway do Olá gerenciamento de API? Posso usá-lo nas regras de firewall?
Nas camadas Standard e Premium Olá, endereço IP público (VIP) saudação do locatário do gerenciamento de API de saudação é estático para tempo de vida de saudação do locatário hello, com algumas exceções. alterações de endereço IP de saudação nessas circunstâncias:

* serviço de saudação é excluído e recriado.
* assinatura do serviço de saudação é [suspenso](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) ou [avisado](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (por exemplo, para nonpayment) e, em seguida, restabelecido.
* Adicionar ou remover a rede Virtual do Azure (você pode usar rede Virtual somente em hello Developer e camada Premium).

Para implantações de várias regiões, Olá alterações de endereço regionais se região Olá é vagas e, em seguida, restabelecido (você pode usar várias regiões implantação somente no nível de Premium Olá).

Locatários da camada Premium configurados para implantação em várias regiões recebem um endereço IP público por região.

Você pode obter seu endereço IP (ou endereços, em uma implantação de várias regiões) na página de locatário Olá Olá portal do Azure.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Posso configurar um servidor de autorização OAUth 2.0 com segurança ADFS?
toolearn como tooconfigure um servidor de autorização OAuth 2.0 com segurança os serviços de Federação do Active Directory (AD FS), consulte [usando o AD FS no gerenciamento de API](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>O método de roteamento de gerenciamento de API usar em localizações geográficas de toomultiple implantações?
Gerenciamento de API usa Olá [método de roteamento de tráfego de desempenho](../traffic-manager/traffic-manager-routing-methods.md#priority) em localizações geográficas de toomultiple de implantações. Tráfego de entrada é roteada toohello gateway de API mais próximo. Se uma região ficar offline, o tráfego de entrada é automaticamente roteado toohello próximo gateway mais próximo. Saiba mais sobre os métodos de roteamentos em [Métodos de roteamento do Gerenciador de Tráfego](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>É possível usar um modelo de Gerenciador de recursos do Azure toocreate uma instância do serviço de gerenciamento de API?
Sim. Consulte Olá [serviço de gerenciamento de API do Azure](http://aka.ms/apimtemplate) modelos de início rápido.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Posso usar um certificado SSL autoassinado para um back-end?
Sim. Aqui está como toouse um autoassinado protocolo (SSL) do certificado para um back-end:

1. Criar uma entidade [back-end](https://msdn.microsoft.com/library/azure/dn935030.aspx) usando o Gerenciamento de API.
2. Saudação de conjunto **skipCertificateChainValidation** propriedade muito**true**.
3. Se você não quiser mais tooallow os certificados autoassinados, excluir a entidade de back-end hello, ou definir Olá **skipCertificateChainValidation** propriedade muito**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Por que recebo uma falha de autenticação quando tento tooclone um repositório Git?
Se você usar o Gerenciador de credenciais de Git, ou se você estiver tentando tooclone um repositório Git usando o Visual Studio, você pode executar em um problema conhecido com a caixa de diálogo de credenciais de Windows hello. caixa de diálogo Olá limita too127 caracteres da senha e truncará senha de gerado pelo Microsoft hello. Estamos trabalhando encurtar senha hello. Por enquanto, use Git Bash tooclone o repositório do Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>O Gerenciamento de API funciona com o Azure ExpressRoute?
Sim. O Gerenciamento de API funciona com o Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Por que exigimos uma sub-rede dedicada em Resource Manager tipo VNETs quando o Gerenciamento de API é implantado nelas?
requisito de sub-rede dedicada Olá para gerenciamento de API vêm de fato hello, ele se baseia no modelo de implantação clássico (camada de PAAS V1). Enquanto estamos pode implantar em um Gerenciador de recursos de VNET (camada V2), há toothat consequências. Olá modelo de implantação clássico no Azure não é acoplado ao modelo do Gerenciador de recursos de saudação e, portanto se você criar um recurso na camada V2, camada de V1 Olá não sabe sobre ele e podem ocorrer problemas, como gerenciamento de API tentar toouse um IP que já está alocado tooa NIC (criado em V2).
toolearn mais sobre a diferença dos modelos clássico e o Gerenciador de recursos no Azure consulte muito[diferença nos modelos de implantação](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Qual é o tamanho de sub-rede mínimo de saudação necessário ao implantar a API de gerenciamento em uma rede virtual?
tamanho de sub-rede mínimo Olá necessário toodeploy gerenciamento de API é [/29](../virtual-network/virtual-networks-faq.md#configuration), que é o tamanho mínimo de sub-rede hello Azure oferece suporte a.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>Pode mover um serviço de gerenciamento de API de um tooanother de assinatura?
Sim. como fazer isso, consulte toolearn [mover recursos tooa novo grupo de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Há restrições ou problemas conhecidos com a importação da minha API?
[Restrições e problemas conhecidos](api-management-api-import-restrictions.md) para formatos Open API (Swagger), WSDL e WADL.
