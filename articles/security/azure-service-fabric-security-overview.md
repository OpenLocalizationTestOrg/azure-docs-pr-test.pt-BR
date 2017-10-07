---
title: "Visão geral de segurança de malha de serviço aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma visão geral da saudação segurança de malha do serviço do Azure."
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
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Visão geral de segurança do Azure Service Fabric
[Malha do Azure do serviço](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implantar e gerenciar serviços de micro escalonáveis e confiáveis. Service Fabric para lidar com desafios significativos de Olá no desenvolvimento e gerenciamento de aplicativos em nuvem. Desenvolvedores e administradores podem evitar problemas complexos de infraestrutura e se concentrarem na implementação de cargas de trabalho essenciais e exigentes que são escalonáveis, confiáveis e gerenciáveis.

Este artigo de visão geral de segurança do Azure Service Fabric enfoca Olá áreas a seguir:

-   Proteção do cluster
-   Monitoramento e diagnóstico
-   Proteção usando Certificados
-   RBAC (Controle de Acesso Baseado em Função)
-   Proteção de cluster usando a segurança do Windows
-   Configuração de segurança de aplicativo no Service Fabric
-   Proteção de comunicação para serviços no Azure Service Fabric Security

## <a name="securing-your-cluster"></a>Proteção do cluster
Azure Service Fabric é um orquestrador de serviços em um cluster de computadores, Clusters devem ser protegido tooprevent não autorizado usuários conectem cluster tooyour, especialmente quando ele tiver cargas de trabalho de produção em execução. Embora seja possível toocreate um cluster não seguro, isso permite que os usuários anônimos tooconnect tooit, se ela expõe toohello de pontos de extremidade de gerenciamento Internet pública.

Esta seção fornece uma visão geral da saudação cenários de segurança para os clusters em execução no Azure ou autônomo e Olá tooimplement de várias tecnologias usadas esses cenários. Olá cenários de segurança de cluster são:

-   Segurança de nó para nó
-   Segurança de cliente para nó

### <a name="node-to-node-security"></a>Segurança de nó para nó
Protege a comunicação entre VMs hello ou máquinas no cluster hello. Isso garante que somente os computadores autorizados toojoin Olá cluster podem participar de hospedar aplicativos e serviços em cluster hello.

Os clusters em execução no Azure ou clusters autônomos em execução no Windows podem usar a [Segurança de Certificado](https://msdn.microsoft.com/library/ff649801.aspx) ou então a [Segurança do Windows](https://msdn.microsoft.com/library/ff649396.aspx) para computadores Windows Server.

**Segurança de certificado de nó para nó**

Serviço de malha usa certificados x. 509 do servidor que você especificar como parte das configurações de tipo de nó hello quando você cria um cluster. Uma visão geral rápida do que são esses certificados e [como você pode adquirir ou criá-los é fornecida neste artigo](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Certificado de segurança é configurada durante a criação de cluster Olá por meio de saudação portal do Azure, modelos do Azure Resource Manager ou um modelo JSON autônoma. É possível especificar um certificado primário e um certificado secundário opcional que é usado para substituições de certificado. Olá certificados primários e secundários que você especificar devem ser diferentes do cliente do administrador de saudação e certificados de cliente somente leitura especificado para [segurança do nó do cliente](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>Segurança de cliente para nó
Segurança de toonode do cliente é configurada usando identidades do cliente. tooestablish relação de confiança entre um cluster de cliente e hello, configure Olá cluster tooknow quais identidades de cliente que pode confiar. Isso pode ser feito de duas maneiras diferentes:

-   Especifique os usuários do grupo de domínio de saudação podem se conectar ou
-   Especifica usuários de nó do domínio Olá podem se conectar.

Malha do serviço oferece suporte a dois tipos de controle de acesso diferentes para os clientes conectados tooa malha do serviço de cluster:

-   Administrador
-   Usuário

Controle de acesso permite Olá Olá tipos cluster administrador toolimit acesso toocertain das operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura. Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação). Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços.

**Segurança de certificado de cliente para nó**

Segurança de certificado de cliente para o nó é configurada durante a criação de cluster Olá por meio de saudação portal do Azure, modelos do Gerenciador de recursos ou um modelo JSON de autônomo, especificando um certificado de cliente de administração e/ou um certificado de cliente do usuário. Olá administrador usuário cliente certificados de cliente e que você especificar devem ser diferentes de certificados primários e secundários Olá especificado para segurança de nó para nó.

Clientes que se conectam usando Olá administrador certificado de cluster de toohello têm recursos de toomanagement de acesso completo. Clientes que se conectam toohello cluster usando o certificado de cliente de usuário somente leitura Olá têm apenas os recursos de toomanagement acesso de leitura. Em outras palavras, que esses certificados são usados para Olá função bases de controle de acesso (RBAC).

Para ler os Azure [configurar um cluster usando um modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn como tooconfigure certificado segurança em um cluster.

**Segurança do AAD (Azure Active Directory) de cliente para nó no Azure**

Clusters em execução no Azure também podem proteger acesso a pontos de extremidade de gerenciamento toohello usando o Azure Active Directory (AAD). Consulte [configurar um cluster usando um modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) para obter informações sobre como toocreate Olá artefatos necessários do AAD, como toopopulate-los durante o cluster de criação e como tooconnect toothose clusters posteriormente.

AAD permite que as organizações (conhecidas como locatários) toomanage usuário acesso tooapplications, que são divididos em aplicativos com um logon baseado na web da interface do usuário e aplicativos com uma experiência de cliente nativo.

Um cluster do Service Fabric oferece várias tooits de pontos de entrada a funcionalidade de gerenciamento, incluindo Olá baseado na web Service Fabric Explorer e Visual Studio. Como resultado, você criar o cluster de toohello do dois AAD aplicativos toocontrol acesso, um aplicativo web e um aplicativo nativo.
Para clusters do Azure, é recomendável que você use o AAD segurança tooauthenticate clientes e certificados para segurança de nó para nó.

Para clusters do Windows Server autônomos, é recomendável usar a segurança do Windows com contas gerenciadas de grupo (GMA) se você tiver o Windows Server 2012 R2 e o Active Directory. Caso contrário, ainda use a segurança do Windows com contas do Windows.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Monitoramento e diagnóstico no Azure Service Fabric
[Monitoramento e diagnóstico](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) são crítico toodeveloping, teste e implantação de aplicativos e serviços em qualquer ambiente. As soluções do Service Fabric funcionam melhor quando você planeja e implementa o monitoramento e o diagnóstico que ajudam a garantir que aplicativos e serviços funcionem conforme o esperado em um ambiente de desenvolvimento local ou na produção.

De uma perspectiva de segurança, Olá principais metas de monitoramento e diagnóstico é para:

-   Detectar e diagnosticar problemas de hardware e a infraestrutura que podem ser devido a eventos de segurança tooa.
-   Detectar problemas de software e o aplicativo que podem fornecer indicadores de comprometimento (IoC).
-   Entender o recurso consumo toohelp impedir acidental de negação de serviço.

Olá fluxo geral de monitoramento e diagnóstico consiste em três etapas:

-   **Geração de eventos:** isso inclui eventos (logs, rastreamentos, eventos personalizados) no nível de aplicativo / serviço e de infraestrutura de saudação (cluster). Leia mais sobre [eventos de nível de infraestrutura](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) e [eventos de nível de aplicativo](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) toounderstand que é fornecido e como tooadd ainda mais a instrumentação.
-   **Agregação de eventos:** eventos gerados necessário toobe coletados e agregados antes que possam ser exibidos. Normalmente, recomendamos usar [diagnóstico do Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (coleta de log baseado em tooagent mais semelhante) ou [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (-processo de coleta de log).
-   **Análise:** eventos necessário toobe visualizados e acessíveis em algum formato, tooallow para análise e exibição conforme necessário. Há várias plataformas grandes que existem no mercado hello quando se trata de toohello análise e à visualização de dados de monitoramento e diagnóstico. Olá dois que recomendamos são [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) e [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) devido tootheir melhor integração com o Service Fabric.

Você também pode usar [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor muitas Olá recursos do Azure no qual um cluster do Service Fabric é criado.

Um watchdog é um serviço separado que pode assistir a integridade e a carga em serviços e a integridade de relatório para qualquer coisa na hierarquia de modelo de integridade de saudação. Isso pode ajudar a evitar erros que não seriam detectados com base no modo de exibição de saudação de um único serviço. Watchdogs também são um bom ponto de código de toohost que executa ações corretivas, sem interação do usuário (por exemplo, a limpeza dos arquivos de log no armazenamento em determinados intervalos de tempo). Você pode encontrar uma implementação de serviço de watchdog de exemplo [aqui](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Proteção usando Certificados
Usar certificados, ele indica como a comunicação entre Olá toosecure Olá vários nós de cluster do Windows autônoma, assim como tooauthenticate os clientes conectados toothis cluster, usando certificados x. 509. Isso garante que somente usuários autorizados possam acessar o cluster de Olá Olá aplicativos implantados e executar tarefas de gerenciamento. Segurança de certificado deve ser habilitada no cluster hello quando Olá cluster é criado.

### <a name="x509-certificates-and-service-fabric"></a>Certificados X.509 e Service Fabric
Certificados digitais x. 509 são usadas tooauthenticate clientes e servidores e tooencrypt e assinem digitalmente as mensagens.

Olá tabela a seguir lista os certificados de saudação necessários na sua configuração de cluster:

|Configuração das Informações de Certificado |Descrição|
|-------------------------------|-----------|
|ClusterCertificate|    Esse certificado é toosecure necessário Olá comunicação entre os nós de saudação em um cluster. Você pode usar dois certificados diferentes, um principal e um secundário para atualização.|
|ServerCertificate| Esse certificado é apresentado toohello cliente quando ele tenta tooconnect toothis cluster. Você pode usar dois certificados de servidor diferentes, um principal e um secundário, para atualização.|
|ClientCertificateThumbprints|  Este é um conjunto de certificados que você deseja tooinstall em clientes Olá autenticado.|
|ClientCertificateCommonNames|  Definir Olá nome comum do certificado de cliente primeiro Olá Olá CertificateCommonName. Olá CertificateIssuerThumbprint é a impressão digital Olá emissor Olá deste certificado.|
|ReverseProxyCertificate|   Este é um certificado opcional que pode ser especificado se você quiser toosecure seu [Proxy Inverter](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Para obter mais informações sobre como proteger os certificados, [clique aqui](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>RBAC (Controle de Acesso Baseado em Função)
Controle de acesso permite Olá administrador toolimit acesso toocertain cluster as operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura. Dois tipos de controle de acesso diferentes têm suporte para clientes que se conectam cluster tooa: função de administrador e a função de usuário.

Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação). Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços.

Você especificar funções Administrador e usuário saudação do cliente em tempo de saudação da criação do cluster, fornecendo identidades separadas (certificados, etc. do AAD) para cada. Para obter mais informações sobre configurações de controle de acesso padrão hello e como toochange Olá configurações padrão, consulte [controle de acesso baseado em função para clientes do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Proteger um cluster autônomo usando a segurança do Windows
tooprevent de cluster de malha do serviço de tooa de acesso não autorizado, você deve proteger o cluster de saudação. Segurança é especialmente importante quando o cluster Olá executa cargas de trabalho de produção. Descreve como a segurança tooconfigure de nó do cliente e de nó para nó usando a segurança do Windows em Olá arquivo Clusterconfig.

**Configurar a segurança do Windows usando gMSA**

Segurança do nó toonode é configurada definindo [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) quando do service fabric precisa toorun em gMSA. Em relações de confiança de toobuild ordem entre os nós, eles devem ser informados uns dos outros.

Segurança de toonode do cliente é configurada usando ClientIdentities. Em ordem tooestablish relação de confiança entre um cluster de cliente e hello, configure Olá cluster tooknow quais identidades de cliente que pode confiar.

**Configurar a segurança do Windows usando um grupo de máquinas**

A segurança do nó toonode é configurada pela configuração usando ClusterIdentity toouse um grupo de computadores em um domínio do Active Directory. Para saber mais, confira [Criar um grupo de máquinas no Active Directory](https://msdn.microsoft.com/library/aa545347).

A segurança de cliente para nó é configurada usando ClientIdentities. tooestablish de confiança entre um cliente e hello cluster, você deve configurar Olá cluster tooknow Olá cliente identidades Olá cluster podem confiar. Você pode estabelecer confiança de duas maneiras diferentes:

-   Especifique os usuários do grupo de domínio de saudação podem se conectar.
-   Especifica usuários de nó do domínio Olá podem se conectar.

## <a name="configure-application-security-in-service-fabric"></a>Configuração de segurança de aplicativo no Service Fabric
### <a name="managing-secrets-in-service-fabric-applications"></a>Gerenciamento de segredos em aplicativos do Service Fabric
Este método ajuda a gerenciar segredos em um aplicativo do Service Fabric. Os segredos podem ser informações confidenciais, como cadeias de conexão de armazenamento, senhas ou outros valores que não devem ser tratados como texto sem formatação.

Essa abordagem usa [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage chaves e segredos. No entanto, usando os segredos em um aplicativo é toobe implantado tooa cluster em nuvem independente de plataforma tooallow aplicativos hospedado em qualquer lugar. Há quatro etapas principais nesse fluxo:

-   Obtenha um certificado de codificação de dados.
-   Instale o certificado de saudação em seu cluster.
-   Criptografar segredos valores ao implantar um aplicativo com o certificado de saudação e colocá-los no arquivo de configuração do serviço Settings.xml.
-   Valores de leitura criptografado fora Settings.xml Descriptografando com hello mesmo certificado de codificação.

>[!Note]
>Saiba mais sobre [Gerenciamento de segredos em aplicativos do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Configurar políticas de segurança para seu aplicativo
Usando a segurança de malha do serviço do Azure, você pode ajudar a proteger aplicativos em execução no cluster de saudação em diferentes contas de usuário. Segurança do serviço de malha também ajuda a certificados, arquivos, diretórios e recursos de saudação seguro que são usados por aplicativos em tempo de saudação da implantação em contas de usuário hello – por exemplo. Isso torna os aplicativos em execução, mesmo em um ambiente hospedado compartilhado, mais protegidos uns dos outros.
Olá etapas incluem:

-   Configure política de saudação para um ponto de entrada de configuração de serviço.
-   Iniciar comandos do PowerShell em um ponto de entrada de instalação.
-   Use o redirecionamento de console para depuração local.
-   Configurar uma política para pacotes de código de serviço.
-   Atribuir uma política de acesso de segurança a pontos de extremidade HTTP e HTTPS.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Proteção de comunicação para serviços no Azure Service Fabric Security
A segurança é um dos aspectos mais importantes de saudação de comunicação. estrutura de aplicativo de serviços confiáveis Olá fornece algumas pilhas de comunicação pré-compilada e ferramentas que podem ser usados tooimprove segurança.

-   [Ajudar a proteger um serviço quando você estiver usando a comunicação remota de serviço](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Ajudar a proteger um serviço quando você estiver usando uma pilha de comunicação baseada em WCF](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Próximas etapas
- Para obter informações conceituais sobre a segurança de cluster, consulte [criar um cluster no Azure usando um modelo do Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) e o [portal do Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Para saber mais consulte [Segurança do cluster do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
