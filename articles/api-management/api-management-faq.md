---
title: Perguntas frequentes sobre Gerenciamento de API do Azure | Microsoft Docs
description: "Conheça as respostas a perguntas comuns, padrões e práticas recomendadas no Gerenciamento de API do Azure."
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
ms.openlocfilehash: a0bf8995913511b0e14304a1259f13de4aa9e04b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-api-management-faqs"></a>Perguntas frequentes sobre Gerenciamento de API do Azure
Obtenha as respostas a perguntas comuns, padrões e práticas recomendadas do Gerenciamento de API do Azure.

## <a name="contact-us"></a>Fale conosco
* [Como fazer uma pergunta à equipe de Gerenciamento de API do Microsoft Azure?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Perguntas frequentes
* [O que significa quando um recurso está em visualização?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Como proteger a conexão entre o gateway de Gerenciamento de API e meus serviços de back-end?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Como copiar minha instância do serviço de Gerenciamento de API para uma nova instância?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [Posso gerenciar minha instância de Gerenciamento de API por meio de programação?](#can-i-manage-my-api-management-instance-programmatically)
* [Como adicionar um usuário ao grupo Administradores?](#how-do-i-add-a-user-to-the-administrators-group)
* [Por que a política que desejo adicionar não está disponível no editor de política?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Como usar o controle de versão de API no Gerenciamento de API?](#how-do-i-use-api-versioning-in-api-management)
* [Como configurar vários ambientes em uma única API?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [Pode usar o SOAP com Gerenciamento de API?](#can-i-use-soap-with-api-management)
* [O endereço IP do gateway do Gerenciamento de API é constante? Posso usá-lo nas regras de firewall?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Posso configurar um servidor de autorização OAUth 2.0 com segurança ADFS?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Que método de roteamento o Gerenciamento de API usa em implantações em vários locais geográficos?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Pode usar um modelo do Azure Resource Manager para criar uma instância do serviço de Gerenciamento de API?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Posso usar um certificado SSL autoassinado para um back-end?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Por que obtenho uma falha de autenticação ao tentar clonar um repositório GIT?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [O Gerenciamento de API funciona com o Azure ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [Por que exigimos uma sub-rede dedicada em Resource Manager tipo VNETs quando o Gerenciamento de API é implantado nelas?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Qual é o tamanho mínimo de sub-rede necessário ao implantar o Gerenciamento de API em uma VNET?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Posso mover um serviço de Gerenciamento de API de uma assinatura para outra?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Há restrições ou problemas conhecidos com a importação da minha API?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-the-microsoft-azure-api-management-team-a-question"></a>Como fazer uma pergunta à equipe de Gerenciamento de API do Microsoft Azure?
Você pode em contato conosco utilizando uma das seguintes opções:

* Poste suas perguntas em nossos [Fórum do MSDN de Gerenciamento de API](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Envie um email a <mailto:apimgmt@microsoft.com>.
* Envie-nos uma solicitação de recurso no [Fórum de comentários do Azure](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>O que significa quando um recurso está em visualização?
Quando um recurso está em visualização, isso significa que estamos buscando ativamente comentários sobre como o recurso está funcionando para você. Um recurso no modo de visualização está funcionalmente completo, mas é possível que façamos uma alteração importante em resposta aos comentários dos clientes. É recomendável que você não dependa de um recurso que está na visualização em seu ambiente de produção. Se você tiver comentários a fazer sobre os recursos de visualização, informe-nos por meio de uma das opções de contato em [Como fazer uma pergunta à equipe de Gerenciamento de API do Microsoft Azure?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services"></a>Como proteger a conexão entre o gateway de Gerenciamento de API e meus serviços de back-end?
Você tem várias opções para proteger a conexão entre o gateway de Gerenciamento de API e os serviços de back-end. Você pode:

* Use a autenticação básica HTTP. Para saber mais, confira [Definir configurações de API](api-management-howto-create-apis.md#configure-api-settings).
* Use a autenticação mútua de SSL conforme descrito em [Saiba como garantir serviços de back-end usando a autenticação de certificado do cliente no Gerenciamento de API do Azure](api-management-howto-mutual-certificates.md).
* Use a lista branca de IPs em seu serviço de back-end. Se você tiver uma instância de Gerenciamento de API de camada Standard ou Premium, o endereço IP do gateway permanecerá constante. Você pode definir sua lista de permissões para permitir esse endereço IP. Você pode obter o endereço IP de sua instância de Gerenciamento de API no painel no portal do Azure.
* Conecte sua instância de Gerenciamento de API a uma Rede Virtual do Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-to-a-new-instance"></a>Como copiar minha instância do serviço de Gerenciamento de API para uma nova instância?
Você tem várias opções para copiar uma instância de Gerenciamento de API para uma nova instância. Você pode:

* Use a função de backup e restauração no Gerenciamento de API. Para saber mais, confira [Como implementar a recuperação de desastre usando restauração e backup de serviço no Gerenciamento de API no Azure](api-management-howto-disaster-recovery-backup-restore.md).
* Criar seu próprio recurso de backup e restauração usando a [API REST de Gerenciamento de API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Use a API REST para salvar e restaurar as entidades da instância do serviço que você deseja.
* Baixe a configuração de serviço usando o Git e carregue-a em uma nova instância. Para obter mais informações, confira [Saiba como salvar e definir a configuração do seu serviço de Gerenciamento de API usando o Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>Posso gerenciar minha instância de Gerenciamento de API por meio de programação?
Sim, você pode gerenciar o Gerenciamento de API de forma programática, usando:

* A [API REST de Gerenciamento de API](https://msdn.microsoft.com/library/azure/dn776326.aspx)
* O [SDK da Biblioteca de Gerenciamento do Serviço Microsoft Azure ApiManagement](http://aka.ms/apimsdk).
* Os cmdlets do PowerShell [Implantação de serviço](https://msdn.microsoft.com/library/mt619282.aspx) e [Gerenciamento de serviço](https://msdn.microsoft.com/library/mt613507.aspx).

### <a name="how-do-i-add-a-user-to-the-administrators-group"></a>Como adicionar um usuário ao grupo Administradores?
Veja como você pode adicionar um usuário ao grupo Administradores:

1. Entre no [Portal do Azure](https://portal.azure.com).
2. Vá para o grupo de recursos que tem a instância de Gerenciamento de API que você deseja atualizar.
3. No Gerenciamento de API, atribua a função **Colaborador de Gerenciamento de Api** ao usuário.

Agora o colaborador recém-adicionado pode usar [cmdlets](https://msdn.microsoft.com/library/mt613507.aspx) do Azure PowerShell. Veja como conectar-se como um administrador:

1. Use o cmdlet `Login-AzureRmAccount` para entrar.
2. Defina o contexto para a assinatura com o serviço usando `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Obter uma única URL de logon usando `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Use a URL para acessar o portal de administração.

### <a name="why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor"></a>Por que a política que desejo adicionar não está disponível no editor de política?
Se a política que você deseja adicionar aparecer esmaecida ou sombreada no editor de política, verifique se você está no escopo correto para a política. Cada declaração de política foi projetada para uso nas seções de política e escopos específicas. Para examinar as seções de política e escopos de uma política, confira a seção de uso da política em [Políticas de Gerenciamento de API](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Como usar o controle de versão de API no Gerenciamento de API?
Você tem algumas opções para usar o controle de versão de API no Gerenciamento de API:

* No Gerenciamento de API, você pode configurar as APIs para representar diferentes versões. Por exemplo, você pode ter duas APIs diferentes, MyAPIv1 e MyAPIv2. Um desenvolvedor pode escolher a versão que deseja usar.
* Você também pode configurar sua API com uma URL de serviço que não inclua um segmento de versão, por exemplo, https://my.api. Em seguida, configure um segmento de versão no modelo [Regravar URL](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) de cada operação . Por exemplo, você pode ter uma operação com um [modelo de URL](api-management-howto-add-operations.md#url-template) chamado /resource e um modelo de [URL de regravação](api-management-howto-add-operations.md#rewrite-url-template) chamado /v1/Resource. Você pode alterar o valor de segmento de versão separadamente para cada operação.
* Se você quiser manter um segmento de versão "padrão" na URL de serviço da API, em operações selecionadas, defina uma política que usa a política [Definir serviço de back-end](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) para alterar o caminho de solicitação de back-end.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Como configurar vários ambientes em uma única API?
Para configurar vários ambientes, por exemplo, um ambiente de teste e um ambiente de produção, em uma única API, você tem duas opções. Você pode:

* Hospede APIs diferentes no mesmo locatário.
* Hospede as mesmas APIs em locatários diferentes.

### <a name="can-i-use-soap-with-api-management"></a>Pode usar SOAP com Gerenciamento de API?
O suporte a [Passagem SOAP](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) agora está disponível. Os administradores podem importar o WSDL do serviço SOAP e o Gerenciamento de API do Azure criará um front-end SOAP. Documentação do portal de desenvolvedor, console de teste, políticas e análise estão disponíveis para serviços SOAP.

### <a name="is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>O endereço IP do gateway do Gerenciamento de API é constante? Posso usá-lo nas regras de firewall?
Nas camadas Standard e Premium, o endereço IP público (VIP) do locatário do Gerenciamento de API é estático para o tempo de vida do locatário, com algumas exceções. O endereço IP é alterado nestas circunstâncias:

* O serviço é excluído e recriado.
* A assinatura do serviço é [suspensa](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) ou [avisada](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (por exemplo, por não pagamento) e, depois, reintegrada.
* Adicionar ou remover a Rede Virtual do Azure (você pode usar a Rede Virtual somente na camada Developer e Premium).

Para implantações de várias regiões, o endereço regional é alterado se a região é desocupada e é restabelecido (você pode usar a implantação de várias regiões apenas na camada Premium).

Locatários da camada Premium configurados para implantação em várias regiões recebem um endereço IP público por região.

Você pode obter seu endereço IP (ou endereços, em uma implantação de várias regiões) na página de locatário no portal do Azure.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Posso configurar um servidor de autorização OAUth 2.0 com segurança ADFS?
Para saber como configurar um servidor de autorização OAuth 2.0 com a segurança do AD FS (Serviços de Federação do Active Directory), confira [Usar ADFS no Gerenciamento de API](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations"></a>Que método de roteamento o Gerenciamento de API usa quando implantado em vários locais geográficos?
O Gerenciamento de API usa o [método de roteamento de tráfego de desempenho](../traffic-manager/traffic-manager-routing-methods.md#priority) em implantações em vários locais geográficos. O tráfego é roteado para o gateway de API mais próximo. Se uma região ficar offline, o tráfego de entrada será automaticamente roteado para o gateway mais próximo. Saiba mais sobre os métodos de roteamentos em [Métodos de roteamento do Gerenciador de Tráfego](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance"></a>Pode usar um modelo do Azure Resource Manager para criar uma instância do serviço de Gerenciamento de API?
Sim. Confira os modelos de Início Rápido do [Serviço de Gerenciamento de API do Azure](http://aka.ms/apimtemplate) .

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Posso usar um certificado SSL autoassinado para um back-end?
Sim. Veja como usar um certificado autoassinado do protocolo SSL (Secure Sockets Layer) para um back-end:

1. Criar uma entidade [back-end](https://msdn.microsoft.com/library/azure/dn935030.aspx) usando o Gerenciamento de API.
2. Defina a propriedade **skipCertificateChainValidation** como **true**.
3. Se você não quiser mais permitir certificados autoassinados, exclua a entidade de back-end ou defina a propriedade **skipCertificateChainValidation** como **false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository"></a>Por que obtenho uma falha de autenticação ao tentar clonar um repositório Git?
Se usar o Gerenciador de Credenciais do Git ou se estiver tentando clonar um repositório Git usando o Visual Studio, você poderá encontrar um problema conhecido com a caixa de diálogo de credenciais do Windows. A caixa de diálogo limita o comprimento da senha a 127 caracteres e trunca a senha gerada pelo Microsoft. Estamos trabalhando para encurtar a senha. Por enquanto, use Git Bash para clonar o repositório Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>O Gerenciamento de API funciona com o Azure ExpressRoute?
Sim. O Gerenciamento de API funciona com o Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Por que exigimos uma sub-rede dedicada em Resource Manager tipo VNETs quando o Gerenciamento de API é implantado nelas?
O requisito de sub-rede dedicado para o Gerenciamento de API vem do fato de ser desenvolvido no modelo de implantação Clássico (camada PAAS V1). Embora possamos implantar em uma VNET do Resource Manager (camada V2), isso tem consequências. O modelo de implantação Clássico no Azure não é rigorosamente acoplado ao modelo do Resource Manager e, portanto, se você criar um recurso na camada V2, a camada V1 não o reconhecerá e isso acarretará problemas, como o Gerenciamento de API tentar usar um IP que já está alocado a uma NIC (desenvolvido em V2).
Para saber mais sobre a diferença dos modelos do Resource Manager e Clássico no Azure, consulte [diferença nos modelos de implantação](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Qual é o tamanho mínimo de sub-rede necessário ao implantar o Gerenciamento de API em uma VNET?
O tamanho mínimo de sub-rede necessário para implantar o Gerenciamento de API é [/29](../virtual-network/virtual-networks-faq.md#configuration), que é o tamanho mínimo de sub-rede que o Azure oferece suporte.

### <a name="can-i-move-an-api-management-service-from-one-subscription-to-another"></a>Posso mover um serviço de Gerenciamento de API de uma assinatura para outra?
Sim. Para saber como, confira [Mover recursos para um novo grupo de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Há restrições ou problemas conhecidos com a importação da minha API?
[Restrições e problemas conhecidos](api-management-api-import-restrictions.md) para formatos Open API (Swagger), WSDL e WADL.
