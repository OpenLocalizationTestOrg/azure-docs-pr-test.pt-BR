---
title: "aaaActive serviços de Federação do diretório no Azure | Microsoft Docs"
description: "Este documento, você aprenderá como toodeploy AD FS no Azure para alta disponibilidade."
keywords: "implantar o AD FS no azure, implantar adfs do azure, o adfs do azure, o azure ad fs, implantar o AD FS, implantar o ad fs, o AD FS no azure, implantar o AD FS no azure, implantar o AD FS no azure, azure AD FS, introdução tooAD FS, Azure, o AD FS no Azure, o iaas, ADFS, mover tooazure adfs"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Implantando os Serviços de Federação do Active Directory no Azure
O AD FS fornece recursos simplificados e seguros de federação de identidade e de logon único (SSO) da Web. Federação com o Azure AD ou O365 permite que os usuários tooauthenticate usando local as credenciais e acessar todos os recursos na nuvem. Como resultado, é importante toohave um altamente disponível do AD FS infraestrutura tooensure acessar tooresources locais e na nuvem hello. Implantar o AD FS no Azure pode ajudar a alcançar alta disponibilidade de saudação obrigatório com esforços mínimo.
Há várias vantagens na implantação do AD FS no Azure. Algumas delas são listadas abaixo:

* **Alta disponibilidade** -com capacidade de saudação de conjuntos de disponibilidade do Azure, você garantir uma infra-estrutura altamente disponível.
* **Fácil tooScale** – precisa de mais desempenho? Migrar facilmente máquinas poderoso toomore por apenas alguns cliques no Azure
* **Redundância geográfica entre** – com o Azure redundância geográfica você pode ter certeza de que sua infraestrutura está altamente disponível globo Olá
* **Fácil tooManage** – com as opções de gerenciamento altamente simplificado no portal do Azure, gerenciar sua infraestrutura é muito fácil e sem complicações 

## <a name="design-principles"></a>Princípios de design
![Design de implantação](./media/active-directory-aadconnect-azure-adfs/deployment.png)

diagrama de saudação acima mostra Olá recomendado toostart topologia básica implantando a infraestrutura do AD FS no Azure. Princípios de saudação por trás da saudação vários componentes de topologia Olá estão listados abaixo:

* **DC/Servidores ADFS**: se tem menos de 1.000 usuários, você pode simplesmente instalar a função do AD FS nos controladores de domínio. Se você não quiser que qualquer impacto no desempenho em controladores de domínio hello, ou se você tiver mais de 1.000 usuários, em seguida, implante o AD FS em servidores separados.
* **Servidor WAP** – é necessário toodeploy servidores de Proxy de aplicativo Web, para que os usuários podem acessar hello quando eles não estão na rede da empresa de saudação também do AD FS.
* **Rede de Perímetro**: servidores de Proxy de aplicativo Web hello serão colocados em Olá DMZ e apenas TCP/443 acesso é permitido entre Olá DMZ e sub-rede interna hello.
* **Balanceadores de carga**: tooensure alta disponibilidade dos servidores do AD FS e Proxy de aplicativo Web, é recomendável usar um balanceador de carga interno para servidores do AD FS e o balanceador de carga do Azure para servidores de Proxy de aplicativo Web.
* **Conjuntos de disponibilidade**: implantação do tooprovide redundância tooyour AD FS, é recomendável agrupar duas ou mais máquinas virtuais em um conjunto de disponibilidade para cargas de trabalho semelhantes. Essa configuração garante que durante um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual esteja disponível
* **Contas de armazenamento**: é recomendável toohave duas contas de armazenamento. Ter uma única conta de armazenamento pode levar toocreation de um ponto único de falha e pode causar Olá toobecome de implantação não está disponível em um cenário improvável onde a conta de armazenamento Olá fica inoperante. Duas contas de armazenamento ajudarão a associar uma conta de armazenamento a cada linha de falha.
* **Segregação de rede**: servidores de Proxy de Aplicativo Web devem ser implantados em uma rede de perímetro separada. Você pode dividir uma rede virtual em duas sub-redes e implantar servidores de Proxy de aplicativo Web de saudação em uma sub-rede a isoladas. Você pode simplesmente definir configurações de grupo de segurança de rede de saudação para cada sub-rede e permitir somente a comunicação necessária entre duas sub-redes de saudação. Mais detalhes são fornecidos para cada cenário de implantação abaixo

## <a name="steps-toodeploy-ad-fs-in-azure"></a>Etapas toodeploy do AD FS no Azure
as etapas Olá mencionadas esta seção da estrutura de tópicos Olá guia toodeploy Olá abaixo descritos a infraestrutura do AD FS no Azure.

### <a name="1-deploying-hello-network"></a>1. Implantação de rede Olá
Conforme descrito acima, você pode criar duas sub-redes em uma única rede virtual ou criar duas redes virtuais completamente diferentes (VNet). Este artigo abordará a implantação de uma única rede virtual e sua divisão em duas sub-redes. Este é uma abordagem mais fácil como dois VNets separadas requerem um gateway de rede virtual tooVNet para comunicações.

**1.1 Criar rede virtual**

![Criar rede virtual](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

Olá portal do Azure, selecione uma rede virtual e você pode implantar uma rede virtual hello e uma sub-rede imediatamente com apenas um clique. Subrede INT também é definido e está pronto para VMs toobe adicionado.
próxima etapa do Hello é tooadd toohello rede de outra sub-rede, ou seja, subrede DMZ de saudação. toocreate Olá sub-rede de rede de Perímetro simplesmente

* Selecione rede Olá recém-criado
* Nas propriedades de saudação selecione subrede
* Na sub-rede Olá painel, clique em Olá adicionar botão
* Forneça Olá sub-rede nome e endereço espaço informações toocreate Olá sub-rede

![Sub-rede](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![Sub-rede de perímetro](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. Criando grupos de segurança de rede Olá**

Um grupo de segurança de rede (NSG) contém uma lista de regras de lista de controle de acesso (ACL) que permitem ou negam o tráfego de rede tooyour instâncias VM em uma rede Virtual. Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede. Quando um NSG está associado uma sub-rede, regras de ACL de saudação se aplicam a instâncias de VM Olá tooall nessa sub-rede.
Para fins de saudação deste guia, vamos criar dois NSGs: uma para uma rede interna e uma rede de Perímetro. Eles serão rotulados como NSG_INT e NSG_DMZ, respectivamente.

![Criar NSG](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

Após Olá que NSG é criado, será 0 regras de saída de entrada e de 0. Depois que as funções hello em servidores do respectivos Olá estiverem instalado e funcional, em seguida, hello regras de entrada e saídas podem ser feitas acordo nível desejado de toohello de segurança.

![Inicializar NSG](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Depois de saudação NSGs são criados, associar NSG_INT sub-rede INT e NSG_DMZ com sub-rede DMZ. Uma captura de tela de exemplo é fornecida abaixo:

![Configurar NSG](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* Clique em sub-redes tooopen Olá painel para sub-redes
* Selecione Olá sub-rede tooassociate com hello NSG 

Após a configuração, o painel Olá para sub-redes deverá parecer como abaixo:

![Sub-redes após NSG](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Criar a Conexão local tooon**

Será necessário um local tooon conexão em ordem toodeploy Olá controlador de domínio (DC) no azure. O Azure oferece várias tooconnect de opções de conectividade seu tooyour de infraestrutura local infraestrutura do Azure.

* Point-to-site
* Rede virtual Site a Site
* ExpressRoute

É recomendável toouse rota expressa. O ExpressRoute permite criar conexões privadas entre os datacenters do Azure e a infraestrutura no local ou em um ambiente de colocalização. Conexões de rota expressa não passam pela Olá Internet pública. Eles oferecem mais confiabilidade, velocidades mais rápidas, latências menores e maior segurança que as conexões típicas pela Internet da saudação.
Embora seja recomendável toouse rota expressa, você pode escolher qualquer método de conexão mais adequado para sua organização. leitura de várias opções de conectividade usando o ExpressRoute, toolearn mais informações sobre a rota expressa e hello [visão geral técnica do ExpressRoute](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Criar contas de armazenamento
Em ordem toomaintain alto de disponibilidade e evitar a dependência de uma única conta de armazenamento, você pode criar duas contas de armazenamento. Dividir máquinas de saudação em cada conjunto de disponibilidade em dois grupos e, em seguida, atribua cada grupo de uma conta de armazenamento separada.

![Criar contas de armazenamento](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Criar conjuntos de disponibilidade
Para cada função (controlador de domínio para o AD FS e WAP), crie conjuntos de disponibilidade com 2 máquinas em Olá mínimo. Isso ajudará a obter maior disponibilidade para cada função. Enquanto conjuntos de disponibilidade de saudação de criação, é essencial toodecide na seguinte hello:

* **Domínios de falha**: máquinas virtuais no mesmo compartilhamento de domínio de falha de Olá Olá a mesma fonte de energia e o comutador de rede física. É recomendável ter no mínimo 2 domínios de falha. valor padrão de saudação é 3 e você pode deixar como está para finalidade de saudação desta implantação
* **Atualizar domínios**: máquinas que pertencem a toohello mesmo domínio de atualização são reiniciados em conjunto durante uma atualização. Você deseja toohave mínimo 2 de domínios de atualização. valor padrão de saudação é 5 e você pode deixar como está para finalidade de saudação desta implantação

![Conjuntos de disponibilidade](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Criar hello seguintes conjuntos de disponibilidade

| Conjunto de disponibilidade | Função | Domínios de falha | Atualizar domínios |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Implantar máquinas virtuais
Olá próxima etapa é máquinas virtuais toodeploy que irá hospedar diferentes funções hello em sua infraestrutura. No mínimo duas máquinas são recomendadas em cada conjunto de disponibilidade. Crie quatro máquinas virtuais para implantação básica do hello.

| Computador | Função | Sub-rede | Conjunto de disponibilidade | Conta de armazenamento | Endereço IP |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |Estático |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |Estático |
| contosowap1 |WAP |Rede de Perímetro |contosowapset |contososac1 |Estático |
| contosowap2 |WAP |Rede de Perímetro |contosowapset |contososac2 |Estático |

Como você deve ter notado, nenhum NSG foi especificado. Isso ocorre porque o azure permite que você use NSG no nível de sub-rede hello. Em seguida, você pode controlar o tráfego de rede de máquina usando Olá que NSG individual associado com a sub-rede hello, caso contrário, objeto NIC hello. Leia mais em [O que é um NSG (grupo de segurança de rede)?](https://aka.ms/Azure/NSG).
Endereço IP estático é recomendável se você estiver gerenciando Olá DNS. Você pode usar o DNS do Azure e em vez disso, nos registros DNS Olá para seu domínio, consulte toohello novas máquinas por seus FQDNs do Azure.
O painel de máquina virtual deve ter aparência abaixo após a implantação de saudação:

![Máquinas Virtuais implantadas](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. Configurar controlador de domínio Olá / servidores do AD FS
 Em ordem tooauthenticate qualquer solicitação de entrada, o AD FS deverá controlador de domínio toocontact hello. toosave hello trip cara de controlador de domínio local tooon do Azure para autenticação, é recomendável toodeploy uma réplica de controlador de domínio Olá no Azure. Em ordem tooattain alta disponibilidade, é recomendável toocreate um conjunto de disponibilidade pelo menos 2 de controladores de domínio.

| Controlador de domínio | Função | Conta de armazenamento |
|:---:|:---:|:---:|
| contosodc1 |Réplica |contososac1 |
| contosodc2 |Réplica |contososac2 |

* Promover dois servidores de saudação como controladores de domínio com DNS
* Configure servidores de saudação do AD FS instalando a função de saudação do AD FS usando o Gerenciador do servidor de saudação.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Implantar o ILB (Balanceador de Carga Interno)
**6.1. Criar hello ILB**

toodeploy um ILB, selecione balanceadores de carga no hello portal do Azure e clique em Adicionar (+).

> [!NOTE]
> Se você não vir **balanceadores de carga** no menu, clique em **procurar** na Olá inferior esquerdo do portal hello e role até que você veja **balanceadores de carga**.  Em seguida, clique em tooadd estrela Olá amarelo-tooyour menu. Agora selecione Olá nova configuração balanceador de carga ícone tooopen Olá painel toobegin saudação do balanceador de carga.
> 
> 

![Procurar balanceador de carga](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **Nome**: dar qualquer balanceador de carga toohello nome adequado
* **Esquema**: desde que este balanceador de carga será colocado na frente de servidores de saudação do AD FS e é destinado para conexões de rede interna apenas, selecione "Interno"
* **Rede virtual**: escolha Olá rede virtual em que você está implantando o AD FS
* **Subrede**: escolha sub-rede interna Olá aqui
* **Atribuição de endereço IP**: estática

![Balanceador de carga interno](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

Depois de clicar em criar e Olá ILB é implantado, você verá na lista de saudação de balanceadores de carga:

![Balanceadores de carga após ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

Próxima etapa é tooconfigure pool de back-end hello e a investigação de back-end de saudação.

**6.2. Configurar pool de back-end ILB**

Selecione hello recém-criado ILB no painel do hello balanceadores de carga. Ele será aberto o painel de configurações do hello. 

1. Selecione pools de back-end do painel de configurações de saudação
2. Em Olá Adicionar painel de pool de back-end, clique em Adicionar a máquina virtual
3. Você verá um painel em que pode escolher o conjunto de disponibilidade
4. Escolha o conjunto de disponibilidade de saudação do AD FS

![Configurar pool ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. Configurando investigação**

No painel de configurações ILB Olá, selecione investigações.

1. Clique em adicionar
2. Fornecer detalhes para investigação a. **Nome**: nome de investigação b. **Protocolo**: TCP c. **Porta**: 443 (HTTPS) d. **Intervalo**: 5 (valor padrão) – é Olá intervalo no qual ILB será investigação máquinas Olá no pool de back-end hello e. **Limite não íntegro**: 2 (padrão val ue) – esse é o limite de saudação de falhas de investigação consecutivas após o qual ILB irá declarar uma máquina no hello back-end pool pare de responder e parar de enviar tráfego tooit.

![Configurar investigação ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. Criar regras de balanceamento de carga**

Em ordem tooeffectively Olá balancear, Olá ILB deve ser configurado com as regras de balanceamento de carga. Em ordem toocreate uma regra de balanceamento de carga 

1. Selecione a regra no painel de configurações de saudação de saudação ILB de balanceamento de carga
2. Clique em Adicionar no hello painel de regra de balanceamento de carga
3. Em Olá Adicionar painel de regra de balanceamento de carga uma. **Nome**: forneça um nome para a regra de saudação b. **Protocolo**: selecione TCP c. **Porta**: 443 d. **Porta de back-end**: 443 e. **Pool de back-end**: selecione Olá pool criado para o AD FS hello cluster f anterior. **Investigação**: teste Olá selecione criado anteriormente para servidores do AD FS

![Configurar regras de balanceamento ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. Atualizar DNS com ILB**

Acesse o servidor DNS tooyour e criar um CNAME para Olá ILB. Olá CNAME deve ser Olá serviço de federação com o endereço IP hello apontando o endereço IP toohello Olá ILB. Por exemplo, se Olá endereço DIP ILB for 10.3.0.8 e o serviço de Federação Olá instalado for fs.contoso.com, em seguida, crie um CNAME para fs.contoso.com apontando too10.3.0.8.
Isso garantirá que todas as comunicações sobre fs.contoso.com terminam em Olá ILB e são adequadamente roteadas.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Configurando o servidor de Proxy de aplicativo Web Olá
**7.1. Configurando Olá Proxy de aplicativo Web tooreach AD FS servidores**

Em ordem tooensure que são servidores de Proxy de aplicativo Web tooreach capaz de servidores de saudação do AD FS por trás de saudação ILB, crie um registro no %systemroot%\system32\drivers\etc\hosts Olá para Olá ILB. Observe que Olá nome diferenciado (DN) deve ser o nome de serviço de Federação hello, por exemplo, fs.contoso.com. E entrada IP hello deve ser de endereço IP do ILB hello (10.3.0.8 como exemplo hello).

**7.2. Instalar função do Proxy de aplicativo Web Olá**

Depois de você garantir que os servidores de Proxy de aplicativo Web tooreach capaz de servidores de saudação do AD FS por trás de ILB, você pode, em seguida, instalar servidores de Proxy de aplicativo Web hello. Servidores de Proxy de aplicativo Web não sejam toohello ingressado no domínio. Instale funções de Proxy de aplicativo Web de saudação em dois servidores de Proxy de aplicativo Web hello, selecionando a função de acesso remoto de saudação. Gerenciador do servidor de saudação vai guiá-lo instalação do toocomplete Olá WAP.
Para obter mais informações sobre como ler toodeploy WAP, [instalar e configurar Olá Web Application Proxy Server](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Implantando Olá balanceador de carga da Internet voltada para (público)
**8.1.  Criar o Balanceador de Carga para a Internet (Público)**

No portal do Azure de Olá, selecione balanceadores de carga e, em seguida, clique em Adicionar. No painel de Balanceador de carga de criar hello, digite Olá informações a seguir

1. **Nome**: nome hello balanceador de carga
2. **Esquema**: público – essa opção informa ao Azure que este balanceador de carga precisará de um endereço público.
3. **Endereço IP**: crie um novo endereço IP (dinâmico)

![Balanceador de Carga para a Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

Após a implantação, o balanceador de carga Olá aparecerá na lista de balanceadores de carga de saudação.

![Lista de balanceadores de carga](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. Atribuir um IP público do rótulo toohello DNS**

Clique na entrada de Balanceador de carga Olá recém-criado no hello balanceadores de carga painel toobring painel Olá para configuração. Execute abaixo do rótulo DNS etapas tooconfigure Olá para o IP público hello:

1. Clique no endereço IP público de saudação. Isso abrirá o painel Olá para o IP público hello e suas configurações
2. Clique em Configuração
3. Forneça um rótulo DNS. Isso tornará o rótulo DNS público Olá que você pode acessar de qualquer lugar, por exemplo contosofs.westus.cloudapp.azure.com. Você pode adicionar uma entrada no hello (contosofs.westus.cloudapp.azure.com) do balanceador de carga de DNS externo para serviço de Federação hello (como fs.contoso.com) que resolve toohello rótulo DNS de saudação externo.

![Configurar balanceador de carga para a Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![Configurar balanceador de carga (DNS) para a Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. Configurar o pool de back-end para o Balanceador de Carga para a Internet (Público)** 

Olá siga mesmo etapas da criação de Balanceador de carga interno hello, pool de back-end tooconfigure Olá para Internet voltada (público) para o balanceador de carga como disponibilidade Olá definido para servidores WAP hello. Por exemplo, contosowapset.

![Configurar pool de back-end do Balanceador de Carga para Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. Configurar investigação**

Siga Olá mesmo as etapas de como configurar Olá de carga interno tooconfigure Olá sonda do balanceador de pool de back-end de saudação do servidores WAP.

![Configurar investigação do Balanceador de Carga para Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. Criar regra(s) de balanceamento de carga**

Siga Olá regra de balanceamento de carga do ILB tooconfigure Olá mesmas etapas para TCP 443.

![Configurar regras de balanceamento do Balanceador de Carga para Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. Proteger a saudação de rede
**9.1. Protegendo a sub-rede interna Olá**

Em geral, você precisa Olá seguindo as regras de tooefficiently proteger sua sub-rede interna (na ordem de saudação como listado abaixo)

| Regra | Descrição | Fluxo |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Permitir a comunicação de HTTPS de saudação do DMZ |Entrada |
| DenyInternetOutbound |Nenhum toointernet de acesso |Saída |

![Regras de acesso INT (entrada)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[comentário]: <> (![regras de acesso INT (entrada)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [comentário]: <> (![regras de acesso INT (saída)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Protegendo a sub-rede de rede de Perímetro Olá**

| Regra | Descrição | Flow |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |Permitir HTTPS da internet toohello DMZ |Entrada |
| DenyInternetOutbound |Qualquer coisa exceto toointernet HTTPS está bloqueada |Saída |

![Regras de acesso EXT (entrada)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[comentário]: <> (![regras de acesso EXT (entrada)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [comentário]: <> (![regras de acesso EXT (saída)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> Se a autenticação de certificado de usuário do cliente (autenticação do clientTLS usando certificados de usuário X509) for necessária, o AD FS exigirá que a porta TCP 49443 seja habilitada para acesso de entrada.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. Logon de saudação do AD FS de teste
Olá, a maneira mais fácil é tootest que AD FS é por meio de saudação IdpInitiatedSignon.aspx página. Em toodo capaz de toobe de ordem, é necessário tooenable Olá IdpInitiatedSignOn nas propriedades de saudação do AD FS. Siga as etapas de saudação abaixo tooverify sua instalação do AD FS

1. Executar Olá abaixo cmdlet no servidor do hello AD FS, usando o PowerShell, tooset-tooenabled.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. De qualquer máquina externa, acesse https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx  
3. Você deve ver a página de saudação do AD FS como abaixo:

![Testar página de logon](./media/active-directory-aadconnect-azure-adfs/test1.png)

Quando você entrar com êxito, ele lhe fornecerá uma mensagem de êxito, conforme mostrado abaixo:

![Êxito do teste](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Modelo de implantação do AD FS no Azure
modelo de saudação implanta uma configuração de 6 máquina, 2 para controladores de domínio, o AD FS e WAP.

[AD FS no modelo de implantação do Azure](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Você pode usar uma rede virtual existente ou criar uma nova VNETao implantar esse modelo. Olá vários parâmetros disponíveis para personalizar a implantação de saudação estão listados abaixo com a descrição de saudação do uso do parâmetro hello no processo de implantação de saudação. 

| Parâmetro | Descrição |
|:--- |:--- |
| Local |recursos de Olá Olá região toodeploy em, por exemplo, Leste dos EUA. |
| StorageAccountType |tipo de saudação do hello conta de armazenamento criada |
| VirtualNetworkUsage |Indica se uma nova rede virtual será criada ou se uma existente será usada |
| VirtualNetworkName |nome de saudação do hello tooCreate de rede Virtual, obrigatório no uso da rede virtual nova ou existente |
| VirtualNetworkResourceGroupName |Especifica o nome de Olá Olá do grupo de recursos onde reside a rede virtual existente do hello. Ao usar uma rede virtual existente, isso se torna um parâmetro obrigatório para que implantação de saudação possa encontrar hello ID de rede virtual existente do hello |
| VirtualNetworkAddressRange |Olá intervalo de endereços de saudação nova rede virtual, obrigatório se criar uma nova rede virtual |
| InternalSubnetName |nome de saudação de sub-rede interna hello, obrigatório em ambas as opções de uso de rede virtual (novas ou existentes) |
| InternalSubnetAddressRange |intervalo de endereços de saudação de sub-rede interna hello, que contém a saudação controladores de domínio e ADFS servidores, obrigatórios se criar uma nova rede virtual. |
| DMZSubnetAddressRange |intervalo de endereços de saudação da sub-rede de rede de perímetro hello, que contém a saudação Windows servidores proxy de aplicativo, obrigatórios se criar uma nova rede virtual. |
| DMZSubnetName |nome de saudação de sub-rede interna hello, obrigatório em ambas as opções de uso de rede virtual (novas ou existentes). |
| ADDC01NICIPAddress |endereço IP interno de saudação do hello primeiro controlador de domínio, esse endereço IP serão estaticamente atribuído toohello controlador de domínio e deve ser um endereço ip válido dentro da sub-rede interna Olá |
| ADDC02NICIPAddress |endereço IP interno de saudação do hello segundo controlador de domínio, esse endereço IP serão estaticamente atribuído toohello controlador de domínio e deve ser um endereço ip válido dentro da sub-rede interna Olá |
| ADFS01NICIPAddress |endereço IP de interno Hello, do primeiro servidor de ADFS Olá, esse endereço IP serão estaticamente atribuído toohello servidor do AD FS e deve ser um endereço ip válido dentro da sub-rede interna Olá |
| ADFS02NICIPAddress |endereço IP de interno Hello, do segundo servidor ADFS Olá, esse endereço IP serão estaticamente atribuído toohello servidor do AD FS e deve ser um endereço ip válido dentro da sub-rede interna Olá |
| WAP01NICIPAddress |endereço IP de interno Hello, do primeiro servidor de WAP Olá, esse endereço IP serão estaticamente atribuído servidor WAP de toohello e deve ser um endereço ip válido dentro da sub-rede de rede de Perímetro Olá |
| WAP02NICIPAddress |Olá interno endereço do segundo servidor WAP hello, esse endereço IP serão estaticamente atribuído servidor WAP de toohello e deve ser um endereço ip válido dentro da sub-rede de rede de Perímetro Olá |
| ADFSLoadBalancerPrivateIPAddress |Balanceador de carga de endereço IP interno de saudação do hello ADFS, esse endereço IP serão estaticamente atribuído toohello balanceador de carga e deve ser um endereço ip válido dentro da sub-rede interna Olá |
| ADDCVMNamePrefix |Prefixo de nome de máquina virtual para controladores de domínio |
| ADFSVMNamePrefix |Prefixo do nome de máquina virtual para servidores ADFS |
| WAPVMNamePrefix |Prefixo do nome de máquina virtual para servidores WAP |
| ADDCVMSize |tamanho da vm saudação do hello controladores de domínio |
| ADFSVMSize |tamanho da vm Olá dos servidores do ADFS Olá |
| WAPVMSize |tamanho da vm Olá dos servidores WAP Olá |
| AdminUserName |nome de saudação do Olá administrador local de máquinas virtuais de saudação |
| AdminPassword |senha Olá Olá conta de administrador local de máquinas virtuais de saudação |

## <a name="additional-resources"></a>Recursos adicionais
* [Conjuntos de Disponibilidade](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [Balanceador de Carga Interno](https://aka.ms/Azure/ILB/Internal)
* [Balanceador de Carga para a Internet](https://aka.ms/Azure/ILB/Internet)
* [Contas de Armazenamento](https://aka.ms/Azure/Storage)
* [Redes Virtuais do Azure](https://aka.ms/Azure/VNet)
* [AD FS e Links de Proxy de Aplicativo Web](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Próximas etapas
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
* [Configurar e gerenciar o AD FS usando o Azure AD Connect](active-directory-aadconnectfed-whatis.md)
* [Implantação do AD FS de alta disponibilidade entre fronteiras geográficas no Azure com o Gerenciador de Tráfego do Azure](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

