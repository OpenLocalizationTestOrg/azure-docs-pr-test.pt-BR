---
title: aaaPublishing aplicativos em redes separadas e locais usando grupos de conector de Proxy de aplicativo do Azure AD | Microsoft Docs
description: Aborda como toocreate e gerenciar grupos de conectores no Proxy de aplicativo do Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publicar aplicativos em redes e locais separados usando grupos de conectores
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Portal clássico do Azure](active-directory-application-proxy-connectors.md)
>

Os clientes utilizam o Proxy de Aplicativo Azure AD para cada vez mais cenários e aplicativos. Então, tornamos o Proxy de Aplicativo ainda mais flexível por meio de mais topologias. Você pode criar grupos de conector de Proxy de aplicativo para que você possa atribuir aplicativos específicos tooserve conectores específicos. Esse recurso fornece mais toooptimize de controle e maneiras de sua implantação do Proxy de aplicativo. 

Cada conector de Proxy de aplicativo é atribuído tooa grupo. Todos os Olá conectores que pertencem a toohello mesmo grupo de conector agir como uma unidade separada para alta disponibilidade e balanceamento de carga. Todos os conectores pertencem tooa grupo. Se você não criar grupos, todos os seus conectores estão em um grupo padrão. Seu administrador pode criar novos grupos e atribuir toothem conectores no hello portal do Azure. 

Todos os aplicativos são atribuídos tooa grupo. Se você não criar grupos, todos os aplicativos são atribuídos tooa grupo de padrão. Mas se você organizar seus conectores em grupos, você pode definir cada toowork de aplicativo com um grupo específico. Nesse caso, somente conectores Olá nesse grupo servem o aplicativo hello mediante solicitação. Esse recurso é útil se os seus aplicativos estiverem hospedados em diferentes locais. Você pode criar grupos de conector com base no local, para que os aplicativos são sempre atendidos pelos conectores que estão fisicamente fechar toothem.

>[!TIP] 
>Se você tiver uma grande implantação do Proxy de aplicativo, não atribua qualquer grupo aplicativos toohello padrão. Dessa forma, novos conectores não recebem qualquer tráfego ao vivo até que você atribua tooan active grupo. Essa configuração também permite que você tooput conectores em um modo ocioso, movendo-os back toohello o grupo padrão, para que você possa executar manutenção sem afetar os usuários.

## <a name="prerequisites"></a>Pré-requisitos
toogroup seus conectores, você tem toomake-se de que você [vários conectores instalados](active-directory-application-proxy-enable.md). Quando você instala um novo conector, ele automaticamente se junta Olá **padrão** grupo.

## <a name="create-connector-groups"></a>Criar grupos de conectores
Use essas etapas toocreate quantos grupos de conector desejado. 

1. Entrar toohello [portal do Azure](https://portal.azure.com).
1. Selecione **Azure Active Directory** > **Aplicativos empresariais** > **Proxy de aplicativo**.
2. Selecione **Novo grupo de conectores**. folha de novo grupo de conector de saudação é exibida.

   ![Selecione o novo grupo de conectores](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. Nomeie seu novo grupo de conector, use Olá suspensa menu tooselect que conectores pertencem a esse grupo.
4. Selecione **Salvar**.

## <a name="assign-applications-tooyour-connector-groups"></a>Atribuir grupos de conector tooyour de aplicativos
Siga estas etapas para cada aplicativo publicado com Proxy de Aplicativo. Você pode atribuir um grupo de conector do aplicativo tooa ao publicá-lo primeiro, ou você pode usar a atribuição de saudação de toochange essas etapas sempre que desejar.   

1. No painel de gerenciamento de saudação do seu diretório, selecione **aplicativos empresariais** > **todos os aplicativos** > Olá aplicativo deseja tooassign tooa conector grupo >  **Proxy de aplicativo**.
2. Saudação de uso **grupo** grupo a lista suspensa menu tooselect Olá ser Olá toouse de aplicativo.
3. Selecione **salvar** tooapply alteração de saudação.

## <a name="use-cases-for-connector-groups"></a>Casos de uso para grupos de conectores 

Os grupos de conectores são úteis para diversos cenários, incluindo:

### <a name="sites-with-multiple-interconnected-datacenters"></a>Sites com vários datacenters interconectados

Muitas organizações têm um número de datacenters interconectados. Nesse caso, você deseja tookeep como a quantidade de tráfego dentro do datacenter Olá possível porque os links entre data centers são caros e lentos. Você pode implantar conectores em cada datacenter tooserve somente Olá aplicativos que residem dentro do datacenter hello. Essa abordagem minimiza os links entre data centers e fornece uma experiência totalmente transparente tooyour usuários.

### <a name="applications-installed-on-isolated-networks"></a>Aplicativos instalados em redes isoladas

Aplicativos podem ser hospedados em redes que não fazem parte da rede corporativa principal de saudação. É possível usar conectores de tooinstall dedicado de grupos de conector em redes isoladas tooalso isolar aplicativos toohello de rede. Isso geralmente acontece quando um fornecedor terceiro mantém um aplicativo específico para sua organização. 

Grupos de conector permitem que você tooinstall dedicado conectores para as redes às quais publicar aplicativos específicos, tornando mais fácil e mais segura do gerenciamento de aplicativos toooutsource toothird fornecedores.

### <a name="applications-installed-on-iaas"></a>Aplicativos instalados no IaaS 

Para aplicativos instalados para o acesso à nuvem IaaS, grupos de conector fornecem um comuns toosecure Olá acesso tooall Olá os aplicativos de serviço. Grupos de conector não criar dependências adicionais em sua rede corporativa ou fragmento de experiência de saudação do aplicativo. Conectores podem ser instalados em cada datacenter na nuvem e servir apenas os aplicativos que residem nessa rede. Você pode instalar vários conectores tooachieve alta disponibilidade.

Tome como exemplo uma organização que tem várias máquinas virtuais conectadas a rede virtual do tootheir próprio IaaS hospedado. tooallow funcionários toouse esses aplicativos, essas redes privadas são conectados toohello rede corporativa usando VPN site a site. Isso proporciona uma boa experiência para os funcionários locais. Mas, ele pode não ser ideal para funcionários remotos, porque isso requer acesso de tooroute de infraestrutura local adicional, como você pode ver no diagrama de saudação abaixo:

![Rede IaaS do Azure](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Com grupos de conector de Proxy de aplicativo do Azure AD, você pode habilitar um serviço toosecure Olá acesso tooall aplicativos comuns sem criar dependências adicionais na sua rede corporativa:

![Fornecedores de várias nuvens de IaaS do AzureAD](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>Várias florestas – grupos de conectores diferentes para cada floresta

A maioria dos clientes que implantou o Proxy de Aplicativo usa seus recursos de SSO (Logon Único) executando a KCD (Delegação restrita de Kerberos). tooachieve isso, máquinas necessidade toobe tooa ingressado no domínio do conector Olá que possa ser delegado a usuários Olá para o aplicativo hello. O KCD oferece suporte a recursos entre florestas. Porém, para as empresas que possuem ambientes diferentes de várias florestas sem qualquer relação de confiança entre eles, é possível usar um único conector para todas as florestas. 

Nesse caso, conectores específicos podem ser implantados por floresta e conjunto tooserve aplicativos que foram publicado tooserve Olá somente os usuários dessa floresta específica. Cada grupo de conectores representa uma floresta diferente. Enquanto o locatário hello e a maioria da experiência de saudação é unificada para todas as florestas, os usuários podem ser atribuídos tootheir aplicativos de floresta usando grupos do AD do Azure.
 
### <a name="disaster-recovery-sites"></a>Sites de Recuperação de Desastre

Há duas abordagens diferentes que podem ser executadas com um site de DR (recuperação de desastres), dependendo de como os sites foram implementados:

* Se seu site de recuperação de desastres é compilado no modo ativo-ativo em que é exatamente como site principal hello e tem Olá mesmo rede e configurações do AD, você pode criar conectores Olá no site Olá DR em Olá mesmo grupo conector de site principal hello. Isso permite que os failovers de toodetect do AD do Azure para você.
* Se seu site de recuperação de desastres é separado do site principal hello, você pode criar um grupo diferente no site Olá DR e o 1) tiver aplicativos de backup ou 2) manualmente desviar Olá existente aplicativo toohello DR grupo conforme necessário.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>Atender a várias empresas de um único locatário

Há várias maneiras diferentes de serviços para várias empresas relacionados ao tooimplement um modelo no qual um provedor de serviço único implanta e mantém o AD do Azure. Grupos de conector ajudam Olá administrador segregar conectores hello e aplicativos em grupos diferentes. Uma forma, que é adequada para pequenas empresas, é toohave um único locatário do Azure AD enquanto empresas diferentes Olá tem seu próprio nome de domínio e redes. Isso também vale para cenários de fusão e aquisição, e situações nas quais uma única divisão de TI atende a várias empresas por motivos regulatórios ou comerciais. 

## <a name="sample-configurations"></a>Exemplos de configuração

Alguns exemplos que você pode implementar, incluem hello seguintes grupos de conector.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>Configuração padrão – não usa grupos de conectores

Se você não usar grupos de conector, sua configuração terá esta aparência:

![AzureAD Sem grupos de conectores](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
Essa configuração é suficiente para testes e pequenas implantações. Ela também funcionará bem se a sua organização tiver uma topologia de rede simples.
 
### <a name="default-configuration-and-an-isolated-network"></a>Configuração padrão e uma rede isolada

Essa configuração é uma evolução da saudação padrão, em que há um aplicativo específico que é executado em uma rede isolada, como a rede virtual IaaS: 

![AzureAD Sem grupos de conectores](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>Configuração recomendada – vários grupos específicos e um grupo padrão para ociosidade

Olá configuração recomendada para organizações grandes e complexas é toohave saudação padrão grupo como um grupo que não atende a todos os aplicativos e é usado para conectores ociosos ou recém-instalado. Todos os aplicativos são atendidos usando grupos de conectores personalizados. Isso permite que toda a complexidade Olá cenários Olá descrito acima.

O exemplo hello abaixo, empresa de saudação tem dois datacenters, A e B, com dois conectores que servem para cada site. Cada site possui aplicativos diferentes em execução. 

![AzureAD Sem grupos de conectores](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>Próximas etapas

* [Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)
* [Habilitar o logon único](application-proxy-sso-overview.md)


