---
title: "práticas recomendadas de segurança do Service Fabric aaaAzure | Microsoft Docs"
description: "Este artigo fornece um conjunto de melhores práticas de segurança do Azure Service Fabric."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Melhores práticas de segurança do Azure Service Fabric
Implantar um aplicativo no Azure é rápido, fácil e econômico. Antes de implantar o aplicativo em nuvem no toohave útil produção uma prática recomendada tooassist na avaliação de seu aplicativo com uma lista de práticas recomendadas essenciais e recomendados.

Malha do serviço do Azure é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implantar e gerenciar microservices escalonável e confiável. Service Fabric também aborda os desafios de saudação significativos no desenvolvimento e gerenciamento de aplicativos em nuvem. Desenvolvedores e administradores podem evitar problemas complexos de infraestrutura e se concentrarem na implementação de cargas de trabalho essenciais e exigentes que são escalonáveis, confiáveis e gerenciáveis. 

Para cada prática recomendada, vamos explicar:

-   A prática recomendada que Olá é
-   Por que você deseja tooenable essa prática recomendada
-   O que pode ser resultado de saudação se você não a prática recomendada de saudação tooenable
-   Como você pode aprender a prática recomendada de saudação tooenable

No momento, temos hello Azure Service Fabric práticas recomendadas de segurança a seguir:

-   Usar o modelo de Manager(ARM) de recursos do Azure e o cluster do Service Fabric do Azure PowerShell Module toocreate seguro
-   Usar certificados X.509
-   Configurar políticas de segurança
-   Configuração de segurança de Reliable Actors
-   Configurar o SSL para o Azure Service Fabric
-   Segurança/isolamento de Rede com o Azure Service Fabric
-   Configurar um cofre de chaves de segurança
-   Atribuir usuários tooroles


## <a name="best-practices-for-securing-your-cluster"></a>Melhores práticas para proteger o cluster

**Visão global**

Usar sempre um cluster seguro
-   Segurança de cluster: usar certificados
-   Acesso de cliente (Admin e Somente leitura): usar o AAD

Usar implantações automatizadas
-   Usar scripts toogenerate, implantar e, sobrepor segredos
-   Manter segredos Olá em KV, use AD todos os outros para acesso de cliente
-   Nenhum humanos devem ter acesso toothem sem autenticação.

Além disso, considere o seguinte hello:
-   Criar DMZs usando NSGs (grupos de segurança de rede)
-   Usar o salto servidores tooRDP em VMs do cluster ou toomanage seu cluster

Clusters devem ser protegido tooprevent não autorizado usuários conectem cluster tooyour, especialmente quando ele tiver cargas de trabalho de produção em execução. Embora seja possível toocreate um cluster não seguro, isso permite que os usuários anônimos tooconnect tooit, se ela expõe toohello de pontos de extremidade de gerenciamento Internet pública.

Tecnologias usadas tooimplement esses cenários. Olá [cenários de segurança de cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) são:

-   Nó para nó segurança This protege a comunicação entre computadores no cluster hello e Olá VMs. Isso garante que somente os computadores autorizados toojoin Olá cluster podem participar de hospedar aplicativos e serviços em cluster hello.
Os clusters em execução no Azure ou clusters autônomos em execução no Windows podem usar a [Segurança de Certificado](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) ou então a [Segurança do Windows](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) para computadores Windows Server.
-   Nó do cliente This segurança protege a comunicação entre um cliente de serviço de malha e nós individuais Olá cluster.
-   Controle de acesso baseado em função (RBAC) - você especificar funções Administrador e usuário saudação do cliente em tempo de saudação da criação do cluster, fornecendo identidades separadas (certificados, etc. do AAD) para cada.
-   Recomendações de segurança-clusters do Azure, é recomendável que você use o AAD segurança tooauthenticate clientes e certificados para segurança de nó para nó.

tooconfigure Olá autônomo cluster do Windows, consulte [configurar as configurações de cluster do windows autônoma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Use modelos do Gerenciador de recursos do Azure e o cluster do Service Fabric do Azure PowerShell Module toocreate seguro.
Um guia passo a passo que orienta você pela configuração de um cluster do Azure Service Fabric seguro no Azure usando o Azure Resource Manager está disponível [aqui](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm).

Usar hello Azure Resource Manager modelo toocustomize seu cluster
-   Armazenamento gerenciado por configuração para VHDs de VM

Use hello Azure Resource Manager modelo toodrive alterações tooyour grupo de recursos
-   Gerenciamento de configuração fácil
-   Auditoria

Tratar a configuração do cluster como código
-   Seja completa na verificação de configurações de saudação escolha toodeploy
-   Evite usar comandos implícita tootweak seus recursos diretamente

Muitos aspectos da saudação [ciclo de vida do aplicativo de malha do serviço](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) pode ser automatizada. O [Módulo Azure PowerShell do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) automatiza tarefas comuns de implantação, atualização, remoção e teste de aplicativos do Service Fabric. APIs gerenciadas e HTTP para gerenciamento de aplicativos também estão disponíveis.

## <a name="use-x509-certificates"></a>Usar certificados X.509
Os clusters sempre devem ser protegidos usando certificados X.509 ou a segurança do Windows. Segurança somente é configurada no momento da criação de cluster e não é possível tooenable segurança depois Olá cluster é criado.

Se você estiver especificando uma [certificado de cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), definir o valor de saudação do ClusterCredentialType tooX509. Se você estiver especificando o certificado do servidor para conexões externas, defina Olá ServerCredentialType tooX509.

-   Os certificados usados em clusters que executam cargas de trabalho de produção devem ser criados por meio de um serviço de certificado do Windows Server configurado corretamente ou obtidos por meio de uma AC (Autoridade de Certificação) aprovada.
-   Nunca use nenhum certificado temporário ou de teste em produção criado com ferramentas como MakeCert.exe.
-   Você pode usar um certificado autoassinado, mas deve fazer isso somente para clusters de teste e não em produção.

Se o cluster de saudação é não segura. Qualquer pessoa pode conectar-se anonimamente e realizar operações de gerenciamento, portanto, os clusters de produção sempre devem ser protegidos usando os certificados x.509 ou a segurança do Windows.

toolearn mais como certificados de tooenable no cluster do service fabric ver, [adicionar ou remover certificados para um cluster do service fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Configurar políticas de segurança
Serviço de malha também ajuda a certificados, arquivos, diretórios e recursos de saudação seguro que são usados por aplicativos em tempo de saudação da implantação em contas de usuário hello – por exemplo. Isso torna os aplicativos em execução, mesmo em um ambiente hospedado compartilhado, mais protegidos uns dos outros.

-   Use um grupo de domínio do Active Directory ou o usuário: você pode executar o serviço de saudação em credenciais Olá para uma conta de usuário ou grupo do Active Directory. Esse é o Active Directory local em seu domínio e não é com o Azure Active Directory (Azure AD). Usando um usuário de domínio ou grupo, em seguida, você pode acessar outros recursos no domínio hello (por exemplo, compartilhamentos de arquivos) que foram concedidos permissões.

-   Atribuir uma política de acesso de segurança para pontos de extremidade HTTP e HTTPS: se você aplicar um serviço de tooa de política de executar como e manifesto do serviço Olá declara recursos de ponto de extremidade com o protocolo de saudação HTTP, você deve especificar um tooensure SecurityAccessPolicy portas alocadas toothese pontos de extremidade estão corretamente acesso controlado listados para Olá conta de usuário RunAs Olá serviço é executado. Caso contrário, o HTTP. sys não tem acesso toohello serviço e obter falhas com chamadas de cliente de saudação.
toolearn mais Habilitar políticas de segurança de malha de serviço, consulte [configurar políticas de segurança para seu aplicativo](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Configuração de segurança de Reliable Actors
Atores confiável do serviço de malha é uma implementação do padrão de design de ator hello. Assim como acontece com qualquer padrão de design de software, decisão Olá se toouse um padrão específico é feito com base em se um software criar problema correspondam padrão de saudação.

Como orientação geral, considere Olá ator padrão toomodel seu problema ou cenário se:
-   Seu problema de espaço envolve um grande número (milhares ou milhões) de pequenas unidades de estado e lógica que, além de serem independentes, são isoladas.
-   Você deseja toowork com objetos de thread único que não exigem interação significativa de componentes externos, incluindo consultando o estado em um conjunto de atores.
-   Suas instâncias de ator não bloquearão chamadores com atrasos imprevisíveis emitindo operações de E/S.

No Service Fabric atores são implementados no framework de Reliable Actors Olá: uma estrutura de aplicativo com base no padrão de ator criada na parte superior do [serviços confiável do serviço do Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Cada serviço escrito do Reliable Actor é, de fato, um Reliable Service com estado particionado.
Cada ator é definido como uma instância de um tipo de ator, toohello idênticos maneira um objeto .NET é uma instância de um tipo .NET. Por exemplo, pode haver um tipo de ator que implementa a funcionalidade de saudação de uma calculadora e pode haver muitos atores desse tipo que são distribuídos em vários nós em um cluster. Cada ator desse é exclusivamente identificado por uma ID de ator.

[As configurações de segurança do replicador](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) são o canal de comunicação do hello toosecure usado é usado durante a replicação. Isso significa que os serviços não consegue ver do outro tráfego de replicação, garantindo que os dados de saudação estará altamente disponíveis também seja seguros. Por padrão, uma seção de configuração de segurança vazia evita a segurança de replicação.
Configurações de replicador configurar replicador de saudação que é responsável por verificar o estado do provedor de estado de ator Olá altamente confiável.

## <a name="configure-ssl-for-azure-service-fabric"></a>Configurar o SSL para o Azure Service Fabric

Autenticação de servidor: [autentica](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) Olá cliente de gerenciamento tooa do pontos de extremidade de gerenciamento de cluster, de forma que hello gerenciamento cliente sabe que está se comunicando cluster real toohello. Esse certificado também fornece um [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) para Olá API de gerenciamento HTTPS em Service Fabric Explorer via HTTPS.
Você deve obter um nome de domínio personalizado para seu cluster. Quando você solicitar um certificado de uma autoridade de certificação, hello nome da entidade do certificado deve corresponder nome de domínio personalizado de saudação que você pode usar para seu cluster.

tooconfigure SSL para um aplicativo, você primeiro precisa tooget um certificado SSL assinado por uma autoridade de certificação (CA), um terceiro confiável que emite certificados para essa finalidade. Se você ainda não tiver um, será necessário tooobtain uma empresa que vende certificados SSL.

certificado de saudação deve atender aos Olá seguindo os requisitos para certificados SSL no Azure:
-   certificado de saudação deve conter uma chave privada.
-   certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).
-   Hello nome da entidade do certificado deve corresponder o serviço de nuvem do hello domínio usado tooaccess hello. Você não pode obter um certificado SSL de uma autoridade de certificação (CA) para o domínio do hello cloudapp.net. Você deve adquirir um toouse de nome de domínio personalizado ao seu serviço de acesso. Quando você solicitar um certificado de uma autoridade de certificação, nome da entidade do certificado Olá deve corresponder Olá domínio personalizado nome usado tooaccess seu aplicativo. Por exemplo, se o nome de domínio personalizado for contoso.com, você pode solicitar um certificado da autoridade de certificação para **.contoso.com** ou **www.contoso.com**
-   certificado Olá deve usar um mínimo de criptografia de 2048 bits.

HTTP é não segura e é o assunto tooeavesdropping ataques porque hello dados sendo transferidos do servidor de web Olá web navegador toohello ou outros pontos de extremidade são transmitidos em texto não criptografado. Isso significa que os invasores podem interceptar e exibir dados confidenciais, como detalhes de cartão de crédito e logons de conta. Quando os dados são enviados ou postados em um navegador usando HTTPS, o protocolo SSL faz com que essas informações sejam criptografadas e fiquem protegidas contra interceptação.

Além disso, consulte toolearn, [configurar SSL para o aplicativo do azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Segurança/isolamento de Rede com o Azure Service Fabric
Use [modelo do Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) como um exemplo para configurar um nodetype três cluster seguro e toocontrol Olá tráfego de rede de entrada e saída usando grupos de segurança de rede.

Olá possui um grupo de segurança de rede para cada Olá escala set(VMSS) toocontrol Olá tráfego de máquina virtual dentro e fora de saudação VMSS. Por padrão, Olá regras são configuradas tooallow que todos Olá tráfego necessário Olá sistema serviços e hello aplicativo portas especificadas no modelo de saudação. Examine essas regras e fazer alterações toofit suas necessidades, incluindo adicionar os novos para seus aplicativos.

Para saber mais, confira [Azure Service Fabric – cenários comuns de rede](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Configurar um cofre de chaves de segurança
Os certificados são usados em Service Fabric tooprovide toosecure de autenticação e criptografia vários aspectos de um cluster e seus aplicativos.

Service Fabric usa toosecure de certificados x. 509 um cluster e fornecer recursos de segurança do aplicativo. Usar o Cofre de chaves muito[gerenciar certificados](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) para clusters de malha do serviço no Azure. Quando um cluster é implantado no Azure, provedor de recursos do Azure de saudação que é responsável pela criação de clusters Service Fabric recebe certificados de Cofre de chaves e os instala no cluster Olá VMs.

Olá a relação entre [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), um cluster do service fabric e o provedor de recursos do Azure Olá que usa certificados armazenados em um cofre de chaves ao criar um cluster.

**Criar um grupo de recursos** Olá primeira etapa é toocreate um grupo de recursos especificamente para o Cofre de chaves. É recomendável que você coloque o Cofre de chaves de saudação em seu próprio grupo de recursos. Essa ação permite remover Olá computação e armazenamento de grupos de recursos, incluindo o grupo de recursos de saudação que contém o cluster do Service Fabric, sem perder suas chaves e segredos. grupo de recursos de saudação que contém seu Cofre de chaves deve estar no hello mesma região Olá cluster que está em uso.

**Criar um cofre de chaves no novo grupo de recursos Olá** Cofre de chaves Olá deve ser habilitado para implantação tooallow Olá certificados de tooget de provedor de recursos de computação-lo e instalá-lo em instâncias de máquina virtual.
toolearn mais como consulte tooset o Cofre de chaves do Azure, [Introdução ao Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Atribuir funções de usuários
Depois que você criou Olá aplicativos toorepresent seu cluster, atribuir usuários toohello funções com suporte do Service Fabric: somente leitura e administrador. Você pode atribuir funções hello usando Olá portal clássico do Azure.

>[!Note]
> Para saber mais sobre as funções no Service Fabric, veja [Controle de acesso baseado em função para clientes do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Malha do serviço do Azure oferece suporte a dois tipos de controle de acesso diferentes para clientes que estão conectado tooa [cluster do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): administrador e usuário. Controle de acesso permite Olá administrador toolimit acesso toocertain cluster as operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura.

## <a name="next-steps"></a>Próximas etapas
- Configurando o [ambiente de desenvolvimento](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started).
- Saiba mais sobre as [opções de suporte do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

