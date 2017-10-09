---
title: "recursos técnicos de segurança aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os serviços que podem ser dimensionada para cima e automaticamente toomeet Olá às necessidades de seu aplicativo ou empresa e serviços de computação em nuvem que incluem uma ampla seleção de instâncias de computação."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Funcionalidades técnicas de segurança do Azure

tooassist atuais e potenciais clientes do Azure entender e utilizar Olá Olá de diversos recursos relacionados à segurança ao redor e disponíveis na plataforma Azure, a Microsoft desenvolveu uma série de White Papers, visões gerais de segurança, as práticas recomendadas, e Listas de verificação. Olá tópicos variam em termos de amplitude e profundidade e são atualizadas periodicamente. Este documento é parte da série, como resumido abaixo da seção abstrata hello. Mais informações sobre esta série sobre a Segurança do Azure podem ser encontradas em (URL).

## <a name="azure-platform"></a>Plataforma do Azure

O [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) é uma plataforma de nuvem composta de serviços de infraestrutura e de aplicativos, com análise avançada e serviços de dados integrados, além de serviços e ferramentas de desenvolvedor, hospedados nos data centers da nuvem pública da Microsoft. Clientes usar o Azure para muitos diferentes recursos e cenários, de computação, rede e armazenamento, toomobile e web aplicativo serviços básicos, cenários de nuvem toofull como Internet das coisas e podem ser usados com as tecnologias de código-fonte aberto e implantados como híbrido nuvem ou hospedado dentro do datacenter do cliente. O Azure fornece a tecnologia em nuvem como blocos de construção toohelp empresas economizar custos, inovem rapidamente e gerenciar os sistemas de maneira proativa. Quando você criar ou migra o provedor de nuvem de tooa de ativos de TI, você depender de tooprotect de recursos da organização seus aplicativos e dados com controles de saudação eles oferecem toomanage Olá segurança de seus ativos com base em nuvem e serviços hello.

Microsoft Azure é Olá somente computação provedor de nuvem que oferece uma plataforma de aplicativo consistente, segura e a infraestrutura-como um serviço para equipes toowork dentro de seus conhecimentos de nuvem diferente e níveis de complexidade do projeto, com dados integrados serviços e análise que descobrem inteligência de dados sempre que existir, Microsoft e plataformas de terceiros, abra estruturas e ferramentas, oferecendo a opção para a integração de nuvem também implantar serviços de nuvem do Azure no local em data centers locais. Como parte da saudação nuvem confiável da Microsoft, os clientes confiam no Azure para segurança do setor, confiabilidade, conformidade, privacidade e Olá ampla rede de pessoas, parceiros e as organizações toosupport de processos na nuvem hello.

Com o Microsoft Azure, você pode:

- Acelere inovação com a nuvem de saudação.

- Impulsionar aplicativos e decisões de negócios com insights.

- Criar livremente e implantar em qualquer lugar.

- Proteger seus negócios.

## <a name="scope"></a>Escopo

o ponto focal de saudação deste white paper relacionado a recursos de segurança e funcionalidade com suporte de componentes do núcleo do Microsoft Azure, ou seja, [armazenamento do Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-introduction), [bancos de dados SQL do Microsoft Azure](https://docs.microsoft.com/azure/sql-database/), [Modelo de máquina virtual do Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/  ), hello e ferramentas e infraestrutura de gerenciamento. Este white paper enfocam tooyou disponível do Microsoft Azure recursos técnicos como clientes toofulfil sua função na proteção de segurança hello e a privacidade de seus dados.

importância de saudação de Noções básicas sobre esse modelo de responsabilidade compartilhada é essencial para os clientes que estão se movendo toohello nuvem. Provedores de nuvem oferecem vantagens consideráveis para os esforços de segurança e conformidade, mas essas vantagens desobriga Prezado cliente de proteção de seus usuários, aplicativos e ofertas de serviço.

Para soluções de IaaS, o cliente de saudação é responsável ou tem a responsabilidade de compartilhado para proteger e gerenciar o sistema de operacional hello, configuração de rede, aplicativos, identidade, clientes e dados.  Criar soluções PaaS em implantações de IaaS, o cliente Olá ainda é responsável ou tem a responsabilidade de compartilhado para proteger e gerenciar aplicativos, identidade, clientes e dados. Para soluções de SaaS, Nonetheless, o cliente Olá continua toobe responsável. Eles devem garantir que os dados são classificados corretamente, e eles compartilham um toomanage responsabilidade seus usuários e dispositivos de ponto de extremidade.

Este documento não oferece cobertura detalhada de qualquer um dos Olá relacionadas a componentes da plataforma Microsoft Azure, como Sites do Azure, Active Directory do Azure, HDInsight, os serviços de mídia e outros serviços que são colocadas em camadas sobre os componentes principais do hello. Embora um nível mínimo de informações gerais seja fornecido, presume-se que os leitores estejam familiarizados com os conceitos básicos do Azure, conforme descritos em outras referências fornecidas pela Microsoft e incluídas em links neste white paper.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>Disponível recursos técnicos toofulfil (cliente) do usuário a responsabilidade de segurança - visão geral

O Microsoft Azure fornece serviços que podem ajudar os clientes atender às necessidades de conformidade, privacidade e segurança de saudação. Olá ajuda a explicar a vários serviços do Azure disponíveis para usuários toobuild uma infraestrutura de aplicativos seguros e são compatíveis com base em padrões do setor de imagem a seguir.

![Funcionalidades técnicas de segurança disponíveis – Um panorama](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>Gerenciar e controlar a identidade e o acesso do usuário (proteger)

Azure ajuda a proteger informações pessoais e negócios, permitindo que você toomanage identidades de usuário e credenciais e controlar o acesso.

### <a name="azure-active-directory"></a>Azure Active Directory

Microsoft identidade e acesso de gerenciamento ajudam a soluções TI proteger acesso tooapplications e recursos em datacenter corporativo hello e em nuvem Olá, habilitando níveis adicionais de validação, como autenticação multifator e condicional políticas de acesso. O monitoramento de atividade suspeita por meio de alertas, auditoria e relatórios de segurança avançados ajuda a reduzir potenciais problemas de segurança. [O Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) fornece toothousands de logon único de aplicativos de nuvem (SaaS) e acesso tooweb aplicativos executados no local.

Benefícios de segurança do Azure AD (Active Directory) incluem a capacidade de saudação:

- Criar e gerenciar uma identidade única para cada usuário em sua empresa híbrida, mantendo usuários, grupos e dispositivos em sincronia.

- Fornece acesso de logon único tooyour aplicativos incluindo milhares de aplicativos SaaS pré-integrados.

- Habilitar a segurança de acesso do aplicativo por meio da imposição da Autenticação Multifator baseada em regras para aplicativos locais e na nuvem.

- Provisionar o acesso remoto seguro local tooon da web de aplicativos por meio do Proxy de aplicativo do Azure AD.

O [portal do Azure Active Directory](http://aad.portal.azure.com/) está disponível como parte do portal do Azure. Deste painel, você pode obter uma visão geral do estado de saudação da sua organização e facilmente aprofundar Gerenciando directory hello, usuários ou acesso de aplicativo.

![Azure Active Directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

A seguir, temos as funcionalidades centrais de gerenciamento de identidade do Azure:

- Logon único

- Autenticação multifator

- Relatórios baseados em aprendizado de máquina, alertas e monitoramento de segurança

- Gerenciamento de acesso e identidade do consumidor

- Registro de dispositivos

- Privileged Identity Management

- Identity Protection

#### <a name="single-sign-on"></a>Logon único

[Sign-on (SSO) único](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) significa que está sendo tooaccess capaz de todos os aplicativos de saudação e recursos que você precisa toodo business, inscrevendo-se apenas uma vez usando uma conta de usuário único. Depois de conectado, você pode acessar todos os aplicativos de saudação sem sendo tooauthenticate necessário (por exemplo, digite uma senha) uma segunda vez.

Muitas organizações contam com aplicativos de SaaS (software como serviço), como o Office 365, o Box e o Salesforce, para aumentar a produtividade do usuário final. Historicamente, IT precisou tooindividually criar e atualizar contas de usuário em cada aplicativo SaaS, e os usuários tinham tooremember uma senha para cada aplicativo SaaS.

[AD do Azure se estende do Active Directory local para nuvem Olá](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), permitindo que usuários toouse seu primário organizacional conta toonot de entrada somente dispositivos que ingressaram no domínio tootheir e recursos da empresa, mas também todos os Olá web e aplicativos SaaS necessário para seu trabalho.

Não apenas os usuários não têm toomanage vários conjuntos de nomes de usuário e senhas, acesso de aplicativo pode ser automaticamente provisionados ou desprovisionados grupos organizacionais com base em e seu status como um funcionário. [O AD do Azure introduz controles de governança de segurança e acesso](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) que permitem que você toocentrally gerenciar o acesso dos usuários nos aplicativos SaaS.

#### <a name="multi-factor-authentication"></a>Autenticação multifator

[Azure multi-factor authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) é um método de autenticação que requer o uso de saudação de mais de um método de verificação e adiciona uma segunda camada crítica de segurança toouser entradas e transações. [A MFA ajuda a proteger](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) acessar aplicativos e toodata atendendo a demanda do usuário para um processo de logon simple. Ela fornece autenticação forte por meio de uma variedade de opções de verificação – chamada telefônica, mensagem de texto, notificação de aplicativo móvel ou código de verificação e tokens OAuth de terceiros.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Relatórios baseados em aprendizado de máquina, alertas e monitoramento de segurança

Monitoramento e alertas de segurança e relatórios baseados no aprendizado de máquina que identificam padrões de acesso inconsistentes podem ajudá-lo a proteger seus negócios. Você pode usar o acesso do Azure Active Directory e uso relatórios toogain visibilidade Olá integridade e segurança do diretório da sua organização. Com essas informações, um administrador de diretório pode determinar melhor onde possíveis riscos de segurança pode para que possa planejar toomitigate adequadamente esses riscos.

No portal clássico do Azure de saudação ou por meio de [portal do Azure Active directory](http://aad.portal.azure.com/), [relatórios](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) são categorizadas em Olá maneiras a seguir:

- Relatórios de anomalias – contêm eventos que encontramos toobe anormais de conexão. Nosso objetivo é toomake você ciente de tais atividades e permitem que você toodecide capaz de toobe sobre se um evento é suspeito.

- Relatórios de aplicativos integrados: fornecem um panorama de como os aplicativos em nuvem estão sendo usados na sua organização. O Active Directory do Azure oferece integração com milhares de aplicativos em nuvem.

- Relatórios de erros – indica os erros que podem ocorrer ao provisionar contas tooexternal aplicativos.

- Relatórios específicos do usuário: exibem dados de atividade de entrada/dispositivo de um usuário específico.

- Logs de atividade – contém um registro de todos os eventos auditados em Olá últimas 24 horas, últimos 7 dias ou últimos 30 dias e alterações do grupo de atividade e atividade de registro e redefinição de senha.

#### <a name="consumer-identity-and-access-management"></a>Gerenciamento de acesso e identidade do consumidor

[B2C de diretório ativo do Azure](https://azure.microsoft.com/services/active-directory-b2c/) é um serviço de gerenciamento de identidades global, altamente disponível para aplicativos voltados para o consumidor que pode ser dimensionado toohundreds de milhões de identidades. Ele pode ser integrado a plataformas móveis e da Web. Seus consumidores podem fazer logon tooall seus aplicativos por meio de experiências personalizáveis com suas contas sociais existentes ou criando novas credenciais.

Em Olá anteriores, os desenvolvedores de aplicativos que desejavam muito[inscrever-se e entrar consumidores](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) em seus aplicativos teria gravado seu próprio código. E teria que usar local bancos de dados ou sistemas toostore nomes de usuário e senhas. B2C de diretório ativo do Azure oferece um melhor forma toointegrate consumidor gerenciamento de identidades em aplicativos com a Ajuda de saudação de uma plataforma segura, baseado em padrões e um grande conjunto de políticas extensíveis de sua organização.

Quando você usa o Azure Active Directory B2C, os consumidores poderão se inscrever nos seus aplicativos usando suas contas sociais existentes (Facebook, Google, Amazon, LinkedIn) ou criando novas credenciais (endereço de email e senha ou o nome de usuário e a senha).

Registro de dispositivos

[O registro de dispositivo do AD do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) é Olá base baseado em dispositivo [acesso condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) cenários. Quando um dispositivo é registrado, o registro de dispositivo do Azure Active Directory fornece dispositivo Olá com uma identidade que é usado tooauthenticate hello quando Olá usuário entra em. dispositivo Olá autenticado e atributos de saudação do dispositivo hello, podem ser usado tooenforce políticas de acesso condicional para aplicativos hospedados na nuvem hello e local.

Quando combinado com um [gerenciamento de dispositivo móvel (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) solução como Intune, os atributos do dispositivo Olá no Active Directory do Azure são atualizados com informações adicionais sobre o dispositivo de saudação. Isso permite regras de acesso condicional toocreate que imponham acesso de dispositivos toomeet aos padrões de segurança e conformidade.

#### <a name="privileged-identity-management"></a>Privileged Identity Management

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) permite gerenciar, controlar e monitorar suas identidades com privilégios e acessar tooresources no AD do Azure bem como outros serviços online da Microsoft como o Office 365 ou Microsoft Intune.

Às vezes, os usuários precisam toocarry operações privilegiadas em recursos do Azure ou Office 365 ou outros aplicativos SaaS. Isso geralmente significa que as organizações têm toogive acesso privilegiado permanente-las no AD do Azure. Esse é um risco de segurança cada vez maior para recursos hospedados em nuvem porque as organizações não podem monitorar de maneira suficiente o que esses usuários estão fazendo com seus privilégios de administrador. Além disso, se uma conta de usuário com acesso privilegiado for comprometida, essa falha poderá afetar a segurança geral da nuvem. O Azure AD Privileged Identity Management ajuda tooresolve esse risco.

O Gerenciamento de identidades com privilégios do AD do Azure:

- Ver quais usuários são administradores do Azure AD

- Habilitar sob demanda "just in time" tooMicrosoft acesso administrativo a serviços Online como o Office 365 e Intune

- Obter relatórios sobre o histórico de acesso de administrador e as alterações nas atribuições de administrador

- Receber alertas sobre a função de tooa de acesso privilegiado

#### <a name="identity-protection"></a>Identity Protection

O [Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) é um serviço de segurança que fornece uma visão consolidada dos eventos de risco e das possíveis vulnerabilidades que afetam as identidades da sua organização. O Identity Protection usa funcionalidades existentes de detecção de anomalias do Azure Active Directory (disponíveis por meio dos Relatórios de Atividade Anômala do Azure AD) e apresenta novos tipos de evento de risco que podem detectar anomalias em tempo real.

## <a name="secured-resource-access-in-azure"></a>Acesso a recursos protegidos no Azure

O controle de acesso no Azure parte de uma perspectiva de cobrança. proprietário de saudação de uma conta do Azure, acessado visitando Olá [Centro de contas Azure](https://account.windowsazure.com/subscriptions), é hello conta AA (administrador). As assinaturas são um contêiner para cobrança, mas também atuam como um limite de segurança: cada assinatura tem um serviço SA (administrador) que pode adicionar, remover e modificar recursos do Azure nessa assinatura usando Olá [portal clássico do Azure](https://manage.windowsazure.com/). Olá SA de padrão de uma nova assinatura é Olá AA, mas Olá AA pode alterar Olá SA no hello Centro de contas do Azure.

![Acesso a recursos protegidos no Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

As assinaturas também têm uma associação com um diretório. diretório de saudação define um conjunto de usuários. Esses podem ser usuários de saudação ou de estudante que criou o diretório hello, ou podem ser usuários externos (ou seja, Accounts da Microsoft). As assinaturas são acessíveis por um subconjunto desses usuários de diretório que foram atribuídos como administrador de serviços (SA) ou CA (Coadministrador); Olá apenas a exceção é que, por razões herdadas, Accounts da Microsoft (anteriormente Windows Live ID) podem ser atribuídas como SA ou CA sem estarem presentes no diretório de saudação.

As empresas orientadas a segurança devem se concentrar em fornecendo aos funcionários permissões exatas de saudação que precisam. Número excessivo de permissões pode expor uma tooattackers de conta. Permissões insuficientes fazem com que os funcionários não consigam trabalhar com eficiência. O [RBAC (controle de acesso baseado em função) do Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) ajuda a resolver esse problema oferecendo gerenciamento de acesso refinado para o Azure.

![Acesso a recursos protegidos ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

Usando o RBAC, você pode separar as tarefas dentro de sua equipe e conceder apenas Olá total acesso toousers que precisam tooperform seus trabalhos. Em vez de apresentar todos irrestrito permissões em sua assinatura do Azure ou recursos, você pode permitir apenas determinadas ações. Por exemplo, use RBAC toolet um funcionário gerenciar máquinas virtuais em uma assinatura, enquanto outro pode gerenciar bancos de dados SQL em Olá mesma assinatura.

![Acesso a recursos protegidos no Azure (RBAC)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Criptografia e segurança de dados no Azure (proteger)

Uma proteção de toodata Olá chaves na nuvem Olá é responsável por possíveis estados Olá na qual os dados podem ocorrer e quais controles estão disponíveis para esse estado. Para criptografia e segurança de dados do Azure melhores práticas recomendadas de saudação ser em torno de saudação estados dos dados a seguir.

- Em repouso: isso inclui todos os objetos de armazenamento, contêineres e tipos de informações que existem estaticamente em mídia física, seja ela magnética ou disco óptico.

- Em trânsito: Quando dados estão sendo transferidos entre componentes, locais ou programas, como rede hello, através de um barramento de serviço (de toocloud local e vice-versa, incluindo conexões híbridas como rota expressa), ou durante uma entrada/saída processo, ele é considerado como sendo em movimento.

### <a name="encryption--rest"></a>Criptografia em repouso

tooachieve criptografia em repouso seguinte hello:

Suporte a pelo menos uma das Olá recomendado modelos de criptografia detalhados Olá tooencrypt dados da tabela a seguir.

| Modelos de criptografia |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| Criptografia de servidor | Criptografia de servidor | Criptografia de servidor | Criptografia de cliente
| Criptografia do lado do servidor usando chaves de serviço gerenciadas | Criptografia do lado do servidor usando chaves gerenciadas pelo cliente no Azure Key Vault | Criptografia do lado do servidor usando chaves gerenciadas pelo cliente no local |
| • Provedores de recursos do azure realizar operações de criptografia e descriptografia de saudação <br> • Microsoft gerencia chaves de saudação <br>• A funcionalidade completa de nuvem | • Provedores de recursos do azure realizar operações de criptografia e descriptografia de saudação<br>• O cliente controla chaves por meio do Cofre de chaves do Azure<br>• Funcionalidade completa na nuvem | • Provedores de recursos do azure realizar operações de criptografia e descriptografia de saudação <br>• O cliente controla as chaves no local <br> • Funcionalidade completa na nuvem| • Os serviços do Azure não podem ver dados descriptografados <br>• Os clientes mantêm as chaves localmente (ou em outros repositórios seguros). As chaves não são serviços tooAzure disponíveis <br>• Funcionalidade reduzida na nuvem|

### <a name="enabling-encryption-at-rest"></a>Habilitando a criptografia em repouso

**Identifique todos os locais em que você armazena dados**

meta de saudação de criptografia em repouso é tooencrypt todos os dados. Isso elimina a possibilidade de saudação de dados importantes ou todos os locais persistentes ausentes. Enumere todos os dados armazenados pelo aplicativo. 

> [!Note] 
> Não apenas "application data" ou "PII', mas nenhum dado relacionado tooapplication incluindo conta metadados (mapeamentos de assinatura, informações de contrato, informações de identificação pessoal).

Considere o que armazena que você estiver usando dados toostore. Por exemplo:

- Armazenamento externo (por exemplo, SQL Azure, DocumentDB, HDInsights, Data Lake etc.)

- Armazenamento temporário (qualquer cache local que inclui dados de locatário)

- Cache na memória (pode ser inserida no arquivo de paginação hello.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Aproveitar a criptografia existente Olá em rest suporte no Azure

Para cada loja que você usar, aproveite Olá existente de criptografia no suporte a Rest.

- Armazenamento do Azure: consulte [Criptografia do Serviço de Armazenamento do Azure para dados em repouso](https://docs.microsoft.com/azure/storage/storage-service-encryption),

- SQL Azure: consulte [TDE (Transparent Data Encryption), SQL Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx)

- Armazenamento em disco local ou em VM ([Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

Para armazenamento em disco local ou em VM, use o Azure Disk Encryption quando houver suporte:

IaaS

Serviços com VMs de IaaS (Windows ou Linux) devem usar [criptografia de disco do Azure](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) tooencrypt volumes que contêm dados do cliente.

PaaS v2

Serviços em execução em PaaS v2 usar o serviço de malha pode usar criptografia de disco do Azure para o conjunto de escala de máquina Virtual [VMSS] tooencrypt suas VMs de v2 PaaS.

PaaS v1

No momento, não há suporte para o Azure Disk Encryption na PaaS v1. Portanto, você deve usar o nível de aplicativo tooencrypt de criptografia de dados em repouso persistentes.  Isso inclui, sem limitações, dados de aplicativos, arquivos temporários, logs e despejos de memória.

A maioria dos serviços deve tentar tooleverage criptografia de saudação de um provedor de recursos de armazenamento. Alguns serviços têm criptografia explícita toodo, por exemplo, qualquer persistentes material de chave (certificados, raiz / mestre chaves) devem ser armazenadas no cofre de chaves.

Se houver suporte a criptografia do lado do serviço com chaves gerenciados pelo cliente deve toobe uma maneira para Olá tooget Olá chave toous. Olá suporte e recomendado toodo de forma que com a integração com o Azure Key Vault (AKV). Nesse caso, os clientes podem adicionar e gerenciar suas chaves no Azure Key Vault. Um cliente pode aprender como toouse AKV via [guia de Introdução ao Cofre de chaves](http://go.microsoft.com/fwlink/?linkid=521402).

toointegrate com o Cofre de chaves do Azure, você poderia adicionar código toorequest uma chave de AKV quando necessário para descriptografia.

- Consulte [Cofre de chaves do Azure – passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) para obter informações sobre como toointegrate com AKV.

Se você oferecer suporte a chaves do cliente gerenciado, você precisa tooprovide um UX para Olá cliente toospecify quais toouse Cofre de chaves (ou URI do Cofre de chave).

Como a criptografia em repouso envolve a criptografia de saudação do host, infraestrutura e locatário dados, perda de saudação de chaves Olá devido a falha de toosystem ou atividade mal-intencionada pode significar todos os dados criptografado de saudação for perdida. Portanto, é essencial que a criptografia em solução de Rest tem uma recuperação de desastre abrangente história falhas toosystem resiliente e atividades mal-intencionadas.

Serviços que implementam a criptografia em repouso geralmente são suscetíveis toohello chaves de criptografia ou dados sendo deixados sem criptografia na unidade de host de saudação (por exemplo, em Olá arquivo de paginação do sistema operacional do host hello.) Portanto, os serviços devem garantir Olá volume de host para seus serviços está criptografado. toofacilitate essa equipe computação tiver habilitado a implantação de saudação de criptografia de Host, que usa [Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP e extensões toohello DCM serviço e agente tooencrypt Olá volume do host.

A maioria dos serviços são implementados em VMs padrão do Azure. Esses serviços devem receber a [Criptografia de host](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) automaticamente quando a computação habilitá-la. Para serviços executados em clusters gerenciados por computação, a criptografia de host será habilitada automaticamente conforme o Windows Server 2016 for distribuído.

### <a name="encryption-in-transit"></a>Criptografia em trânsito

A proteção dos dados em trânsito deve ser parte essencial de sua estratégia de proteção de dados. Desde que os dados se movem para a frente e para trás em vários locais, a recomendação geral Olá é sempre usar dados de tooexchange protocolos SSL/TLS em diferentes locais. Em algumas circunstâncias, talvez seja o canal de comunicação inteira Olá tooisolate entre seu local e nuvem infraestrutura usando uma rede virtual privada (VPN).

Para dados que se movem entre sua infraestrutura local e o Azure, você deve considerar proteções adequadas, como HTTPS ou VPN.

Para organizações que precisam de acesso toosecure de vários tooAzure localizado no local de estações de trabalho, use [VPN site a site do Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Para organizações que precisam de acesso toosecure de uma estação de trabalho localizado no local tooAzure, use [ponto a Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Conjuntos de dados maiores podem ser movidos em um link WAN de alta velocidade dedicado, como o [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Se você escolher toouse rota expressa, você também pode criptografar dados Olá no nível do aplicativo, Olá usando [SSL/TLS](https://support.microsoft.com/kb/257591) ou outros protocolos para proteção adicional.

Se você estiver interagindo com o armazenamento do Azure por meio de saudação Portal do Azure, todas as transações ocorrem por meio de HTTPS. [API de REST do armazenamento](https://msdn.microsoft.com/library/azure/dd179355.aspx) via HTTPS também pode ser o toointeract usado com [armazenamento do Azure](https://azure.microsoft.com/services/storage/) e [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/).

As organizações que não tooprotect dados em trânsito são mais suscetíveis para [ataques man-in-the-middle](https://technet.microsoft.com/library/gg195821.aspx), [espionagem](https://technet.microsoft.com/library/gg195641.aspx)e sequestro de sessão. Esses ataques podem ser a primeira etapa Olá na obtenção de dados do access tooconfidential.

Você pode aprender mais sobre a opção de VPN do Azure lendo o artigo Olá [de planejamento e design para o Gateway de VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).

### <a name="enforce-file-level-data-encryption"></a>Impor criptografia de dados no nível do arquivo

[O Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp de políticas de criptografia, identidade e autorização usa proteger seus arquivos e email. O Azure RMS funciona em vários dispositivos, como telefones, tablets e PCs, protegendo-os dentro e fora da sua organização. Esse recurso é possível porque o Azure RMS adiciona um nível de proteção permanece com dados hello, mesmo quando ele sai dos limites da organização.

Quando você usa o Azure RMS tooprotect seus arquivos, você está usando criptografia padrão do setor com suporte total a [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Quando você utilizar o Azure RMS para proteção de dados, terá garantia Olá que Olá permanece com arquivo hello, mesmo se ele for copiado toostorage que não está sob controle de saudação de TI, como um serviço de armazenamento de nuvem. Olá mesmo ocorre para os arquivos compartilhados por email, Olá arquivo é protegido como uma mensagem de email do anexo tooan, com instruções como tooopen Olá protegido anexo.
Ao planejar para a adoção do Azure RMS, é recomendável seguir hello:

- Instalar Olá [aplicativo RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Esse aplicativo se integra a aplicativos do Office, instalando um suplemento do Office para que os usuários possam proteger seus arquivos de forma direta e fácil.

- Configurar aplicativos e serviços toosupport Azure RMS

- Crie [modelos personalizados](https://technet.microsoft.com/library/dn642472.aspx) que reflitam as necessidades dos negócios. Por exemplo: um modelo de dados secretos que deve ser aplicado a todos os emails secretos relacionados.

As organizações que são fracas em [classificação de dados](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) e proteção de arquivo pode ser mais suscetível vazamento de toodata. Sem proteção adequadas de arquivo, as organizações não ser capaz de tooobtain ideias de negócios, monitorar abuso e impedir o acesso mal-intencionado toofiles.

> [!Note]
> Você pode aprender mais sobre o Azure RMS ao ler o artigo Olá [guia de Introdução ao Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

## <a name="secure-your-application-protect"></a>Proteger seu aplicativo (proteção)
Enquanto o Azure é responsável por proteger infraestrutura hello e que seu aplicativo é executado na plataforma, é sua responsabilidade toosecure seu próprio aplicativo. Em outras palavras, você precisa toodevelop, implantar e gerenciar o código do aplicativo e o conteúdo de forma segura. Sem isso, o código do aplicativo ou o conteúdo ainda pode ser vulnerável toothreats.

### <a name="web-application-firewall-waf"></a>Firewall do aplicativo Web (WAF)
O [WAF (firewall do aplicativo Web)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) é um recurso do [Gateway de Aplicativo](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) que fornece proteção centralizada de seus aplicativos Web contra vulnerabilidades e explorações comuns.

Firewall do aplicativo Web é baseada em regras de saudação [conjuntos de regras de núcleo OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 ou 2.2.9. Os aplicativos Web cada vez mais são alvos de ataques mal-intencionados que exploram vulnerabilidades conhecidas comuns. São comuns entre essas explorações ataques de injeção SQL, script entre sites ataques tooname alguns. Evitar tais ataques no código do aplicativo pode ser desafiadora e pode exigir a manutenção rigorosa, aplicação de patch e monitoramento em vários níveis de topologia de aplicativo hello. Um firewall do aplicativo web centralizado ajuda a simplificar o gerenciamento de segurança muito mais simples e oferece aos administradores de tooapplication contra ameaças ou invasões de garantia melhor. Uma solução WAF também possa reagir de ameaça à segurança tooa mais rápida por uma vulnerabilidade conhecida em um local central em vez de proteção de cada um dos aplicativos web individuais de aplicação de patch. Os gateways de aplicativos existentes podem ser facilmente convertido tooa web aplicativo firewall habilitado application gateway.

Algumas das vulnerabilidades web comuns Olá quais firewall do aplicativo web protege contra inclui:

- Proteção contra injeção de SQL

- Proteção contra scripts entre sites

- Proteção Contra Ataques Comuns da Web, como a injeção de comandos, as solicitações HTTP indesejadas, a divisão de resposta HTTP e o ataque de inclusão de arquivo remoto

- Proteção contra violações de protocolo HTTP

- Proteção contra anomalias de protocolo HTTP, como ausência de host de agente do usuário e de cabeçalhos de aceitação

- Prevenção contra bots, rastreadores e scanners

- Detecção de problemas de configuração de aplicativo comuns (ou seja, Apache, IIS etc.)

> [!Note]
> Para uma lista mais detalhada das regras e suas proteções consulte seguinte Olá [principais conjuntos de regras](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

O Azure também fornece várias toohelp de fácil de usar recursos proteger o tráfego de entrada e saído para seu aplicativo. Azure também ajuda os clientes proteger seu código de aplicativo, fornecendo externamente fornecida funcionalidade tooscan seu aplicativo web para vulnerabilidades.

- [Proteger seu aplicativo Web usando vários meios de autenticação e autorização](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [Configurar a autenticação do Active Directory do Azure para seu aplicativo](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [Proteger o tráfego tooyour aplicativo habilitando Transport Layer Security (TLS/SSL) - HTTPS](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [Forçar todo o tráfego recebido por conexão HTTPS](http://microsoftazurewebsitescheatsheet.info/)

  - [Habilitar HSTS (Segurança de Transporte Estrito)](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [Restringir acesso tooyour aplicativo pelo endereço IP do cliente](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [Restringir acesso tooyour aplicativo o comportamento do cliente - frequência de solicitação e simultaneidade](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Examinar o código do aplicativo Web em busca de vulnerabilidades usando a Tinfoil Security Scanning](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [Configurar TLS autenticação mútua toorequire cliente certificados tooconnect tooyour aplicativo web](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Configurar um certificado de cliente para uso em seu aplicativo toosecurely tooexternal recursos de conexão](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [Remover as ferramentas de tooavoid de cabeçalhos padrão do servidor de impressão digital do seu aplicativo](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [Conectar seu aplicativo com segurança com recursos em uma rede privada usando VPN Ponto a Site](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [Conectar seu aplicativo com segurança com recursos em uma rede privada usando Conexões Híbridas](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Usos de serviço de aplicativo do Azure Olá mesma solução Antimalware usada por serviços de nuvem do Azure e máquinas virtuais. toolearn mais sobre isso consulte tooour [Antimalware documentação](https://docs.microsoft.com/azure/security/azure-security-antimalware).

## <a name="secure-your-network-protect"></a>Proteger sua rede (proteção)
Microsoft Azure inclui um toosupport robusta de infraestrutura de rede de seu aplicativo e os requisitos de conectividade do serviço. Conectividade de rede é possível entre os recursos localizados no Azure, entre locais e hospedado do Azure, recursos e tooand de saudação à Internet e o Azure.

Olá [infra-estrutura de rede do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) permite que você toosecurely conectar recursos do Azure tooeach com outros [redes virtuais (VNets)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Uma rede virtual é uma representação de sua própria rede na nuvem hello. Uma rede virtual é uma isolamento lógico de assinatura de tooyour de rede dedicada Olá nuvem do Azure. Você pode se conectar a redes de local de tooyour VNets.

![Proteger sua rede (proteção)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

Se você precisa de controle de acesso no nível de rede básica (com base em protocolos IP de endereço e saudação TCP ou UDP), você pode usar [grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg). Um grupo de segurança de rede (NSG) é um pacote com monitoração de estado básico firewall de filtragem e permite que você toocontrol acesso com base em um [5-tupla](https://www.techopedia.com/definition/28190/5-tuple).

Rede do Azure oferece suporte ao comportamento de roteamento do hello capacidade toocustomize Olá para o tráfego de rede em suas redes virtuais do Azure. É possível fazer isso configurando [Rotas Definidas pelo Usuário](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) no Azure.

[Encapsulamento forçado](https://www.petri.com/azure-forced-tunneling) é um mecanismo que você pode usar tooensure seus serviços não são permitidos tooinitiate toodevices uma conexão em Olá da Internet.

Dá suporte ao Azure dedicado a rede local do link WAN conectividade tooyour e uma rede Virtual do Azure com [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Olá link entre o Azure e seu site usa uma conexão dedicada que não passa pelo Olá Internet pública. Se seu aplicativo do Azure é executado em vários datacenters, você pode usar [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute solicitações de usuários de forma inteligente entre instâncias do aplicativo hello. Você também pode rotear o tráfego tooservices não em execução no Azure, se eles são acessíveis de saudação à Internet.

## <a name="virtual-machine-security-protect"></a>Segurança de máquina virtual (proteger)

As [máquinas virtuais do Azure](https://docs.microsoft.com/azure/virtual-machines/) permitem que você implante uma ampla gama de soluções de computação de forma ágil. Com suporte para o Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP e Serviços BizTalk do Azure, você pode implantar qualquer carga de trabalho e qualquer linguagem em praticamente qualquer sistema operacional.

Com o Azure, você pode usar [software antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) de fornecedores de segurança, como Microsoft, Symantec, Trend Micro e Kaspersky tooprotect suas máquinas virtuais de arquivos mal-intencionados, adware e outras ameaças.

O Microsoft Antimalware para Serviços de Nuvem e Máquinas Virtuais do Azure é uma funcionalidade de proteção em tempo real que ajuda a identificar e remover vírus, spyware e outros softwares mal-intencionados. O Antimalware da Microsoft fornece alertas configuráveis conhecido tooinstall de tentativas de software mal-intencionado ou indesejado em si ou executar em seus sistemas do Azure.

O [Backup do Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) é uma solução escalonável que protege os dados de seu aplicativo sem nenhum investimento de capital e com custos operacionais mínimos. Erros de aplicativo podem corromper seus dados e erros humanos podem introduzir bugs em seus aplicativos. Com o Backup do Azure, suas máquinas virtuais executando Windows e Linux estão protegidas.

O [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) ajuda a orquestrar a replicação, failover e recuperação dos aplicativos e cargas de trabalho para que eles estejam disponíveis a partir de um local secundário, caso o local principal fique inativo.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>Garantia de conformidade: lista de verificação de inspeção detalhada dos serviços de nuvem (proteger)

Microsoft desenvolvido [Olá nuvem serviços devido cuidado lista de verificação](https://aka.ms/cloudchecklist.download) tomou as organizações toohelp cuidado ao considerar uma nuvem de toohello move. Ele fornece uma estrutura para uma organização de qualquer tamanho e tipo — privadas empresas e organizações do setor público, incluindo governamentais e em todos os níveis de organizações sem fins lucrativos — tooidentify seus próprios desempenho, serviços, gerenciamento de dados e os objetivos de controle e requisitos. Isso permite que as ofertas de saudação toocompare dos provedores de serviços de nuvem diferente, formando, por fim, a base de saudação para um contrato de serviço de nuvem.

lista de verificação de saudação fornece uma estrutura que atenda a cláusula a cláusula com um novo padrão internacional para contratos de serviço de nuvem, ISO/IEC 19086. Esse padrão oferece um conjunto unificado de considerações para organizações toohelp-los a tomar decisões sobre adoção da nuvem e criar uma base comum para comparação de ofertas de serviço de nuvem.

lista de verificação de saudação promove uma nuvem de toohello mover completamente verificados, fornecendo orientação estruturada e uma abordagem consistente e reproduzível para escolher um provedor de serviços de nuvem.

A adoção da nuvem não é simplesmente uma decisão tecnológica. Porque a lista de verificação requisitos falam sobre todos os aspectos de uma organização, eles servem tooconvene todas as chaves internos-tomadores de decisão — hello CIO e CISO, bem como informações jurídicas, corre o risco de profissionais de gerenciamento, a aquisição e a conformidade. Isso aumenta a eficiência de saudação do processo de tomada de decisão hello e decisões Terra som raciocínio, reduzindo a probabilidade de saudação de problemas imprevistos tooadoption.

Além disso, Olá lista de verificação:

- Expõe os tópicos de discussão de chave para responsáveis pelas decisões no início do processo de adoção de nuvem Olá Olá.

- Oferece suporte a discussões de negócios completa sobre normas e os objetivos da organização Olá para privacidade, informações de identificação pessoal (PII) e segurança de dados.

- Ajuda as organizações a identificar problemas potenciais que podem afetar um projeto de nuvem.

- Fornece um conjunto consistente de perguntas com hello mesmo termos, definições, métricas e os resultados para cada provedor, o processo de saudação toosimplify de comparação de ofertas de provedores de serviços de nuvem diferente.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Validação de segurança de aplicativo e infraestrutura do Azure (detectar)

[Segurança operacional Azure](https://docs.microsoft.com/azure/security/azure-operational-security) refere-se serviços toohello, controles e toousers de recursos disponíveis para proteger seus dados, aplicativos e outros recursos do Microsoft Azure.

![Validação de segurança (detectar)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Segurança operacionais do Azure é construída em uma estrutura que incorpora conhecimento Olá obtido por meio de uma diversos recursos que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Centro de resposta de segurança do Microsoft programa e conhecimento profundo do cenário de ameaças de segurança cibernética hello.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft OMS (Operations Management Suite)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) é hello solução de gerenciamento de TI para a nuvem híbrida de saudação. Usada sozinha ou tooextend sua implantação do System Center existente, o OMS oferece Olá máxima flexibilidade e controle de gerenciamento baseado em nuvem de sua infraestrutura.

![Microsoft OMS (Operations Management Suite)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

Com o OMS, você pode gerenciar qualquer instância em qualquer nuvem, incluindo local, Azure, AWS, Windows Server, Linux, VMware e OpenStack, com um custo menor do que as soluções dos concorrentes. Projetado para nuvem Olá, mundo, o OMS oferece um novo toomanaging de abordagem sua empresa que é hello mais rápida e mais econômica maneira toomeet novos negócios desafios e acomodar novas cargas de trabalho, aplicativos e ambientes de nuvem.

### <a name="log-analytics"></a>Log Analytics

O [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornece serviços de monitoramento para o OMS coletando dados de recursos gerenciados em um repositório central. Esses dados podem incluir eventos, dados de desempenho ou dados personalizados fornecidos por meio da API de saudação. Depois de coletados, dados saudação estão disponíveis para alertas, análise e exportação.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

Esse método permite que você tooconsolidate dados de uma variedade de fontes, para que você pode combinar dados de seus serviços do Azure com seus ambientes locais. Ele também separa coleção Olá dos dados Olá pela ação de saudação executada com os dados para que todas as ações disponíveis tooall tipos de dados.

### <a name="azure-security-center"></a>Central de Segurança do Azure

[Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) Olá de ajuda a evitar, detectar e responder toothreats maior visibilidade e controle sobre a segurança de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

Central de segurança analisa o estado de segurança Olá seus recursos do Azure tooidentify possíveis vulnerabilidades de segurança. Uma lista de recomendações orienta você pelo processo de saudação de configuração de controles necessários.

Os exemplos incluem:

- Provisionamento antimalware toohelp identificar e remover softwares mal-intencionados

- Configurando a rede segurança e grupos de regras toocontrol tráfego tooVMs

- Provisionamento de firewalls de aplicativo web toohelp se proteger contra ataques que seus aplicativos web de destino

- Como implantar atualizações de sistema ausentes

- Configurações de sistema operacional que não correspondem a saudação de endereçamento recomendado linhas de base

Central de segurança automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede hello e soluções de parceiros, como programas de antimalware e firewalls. Quando forem detectadas ameaças, é criado um alerta de segurança. Os exemplos abrangem a detecção de:

- As máquinas virtuais comprometidas se comunicam com os endereços IP mal-intencionados conhecidos

- Malware avançado detectado usando o relatório de erros do Windows

- Ataques por força bruta contra máquinas virtuais

- Alertas de segurança dos firewalls e programas antimalware integrados

### <a name="azure-monitor"></a>Azure Monitor

[Monitor do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) fornece tooinformation ponteiros em tipos específicos de recursos. Ele oferece visualização, consulta, roteamento, alertas, AutoEscala e automação em dados de saudação infraestrutura do Azure (Log de atividade) e cada recurso do Azure individual (Logs de diagnóstico).

Os aplicativos em nuvem são complexos com muitas partes móveis. O monitoramento fornece tooensure de dados que seu aplicativo permaneça ativo e em execução em um estado íntegro. Ele também ajuda você toostave off problemas potenciais ou solucionar problemas após os.

![Monitor do Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) Além disso, você pode usar o monitoramento dados toogain aprofundamento sobre seu aplicativo. Esse conhecimento pode ajudá-lo a facilidade de manutenção ou de desempenho do aplicativo tooimprove, ou automatizar ações que normalmente exigiriam a intervenção manual.

A auditoria da segurança de sua rede é fundamental para detectar vulnerabilidades de rede e garantir a conformidade com o modelo de governança regulatória e segurança de TI. Com a exibição de grupo de segurança, você pode recuperar as regras de grupo de segurança de rede e segurança Olá configurado, bem como Olá regras de segurança efetivo. Lista de saudação de regras aplicadas, você pode determinar ss e portas Olá abertas vulnerabilidade de rede.

### <a name="network-watcher"></a>Observador de Rede

[Inspetor de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) é um serviço regional que permite que você toomonitor e diagnosticar as condições em um nível de rede no e do Azure. Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure. Esse serviço inclui a captura de pacotes, próximo salto, verificação do fluxo de IP, exibição do grupo de segurança e logs de fluxo de NSG. Monitoramento do nível do cenário fornece uma exibição de tooend final dos recursos de rede no monitoramento de recursos de rede do contraste tooindividual.

### <a name="storage-analytics"></a>Análise de armazenamento

[Análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) pode armazenar métricas que incluem dados de estatísticas e a capacidade de transações agregadas sobre o serviço de armazenamento de tooa solicitações. As transações são relatadas no nível de operação ambos Olá API, bem como no nível de serviço de armazenamento hello e capacidade é relatada no nível de serviço de armazenamento de saudação. Dados de métrica pode ser usado tooanalyze uso do serviço de armazenamento, diagnosticar problemas com solicitações feitas no serviço de armazenamento hello e desempenho de saudação tooimprove dos aplicativos que usam um serviço.

### <a name="application-insights"></a>Application insights

O [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) é um serviço APM (Gerenciamento de Desempenho de Aplicativos) extensível para desenvolvedores da Web em várias plataformas. Use-toomonitor seu aplicativo web em tempo real. Ele detectará anomalias de desempenho automaticamente. Ele inclui uma análise rigorosa ferramentas toohelp que diagnosticar problemas e toounderstand que os usuários fazem com seu aplicativo. Ele é projetado toohelp você continuamente melhorar o desempenho e usabilidade. Ele funciona para aplicativos em uma ampla variedade de plataformas, incluindo .NET, Node.js e J2EE, hospedado no local ou na nuvem hello. Ele se integra ao seu processo de devOps e tem várias ferramentas de desenvolvimento de tooa de pontos de conexão.

Ele monitora:

- **Taxas de solicitação, tempos de resposta e taxas de falha** - descubra quais páginas estão mais populares, em que momentos do dia, e onde os usuários estão. Confira as páginas que têm melhor desempenho. Se as taxas de falha e os tempos de resposta ficam altos quando há mais solicitações, possivelmente você tem um problema de alocação de recursos.

- **Taxas de dependência, tempos de resposta e taxas de falha** - descubra se os serviços externos estão atrasando você.

- **Exceções** - analisar estatísticas agregada de saudação, ou selecionar instâncias específicas e analisar o rastreamento de pilha hello e solicitações relacionadas. A maioria das exceções de navegador e servidor são relatadas.

- **Exibições de página e o desempenho de carregamento** - relatados por navegadores dos usuários.

- **Chamadas AJAX de páginas da Web** – taxas, tempos de resposta e taxas de falha.

- **Contagens de sessão e usuários.**

- **Contadores de desempenho** de suas máquinas de servidor Linux ou Windows server, como CPU, memória e uso da rede.

- **Diagnósticos de host** do Docker ou do Azure.

- **Logs de rastreamento de diagnóstico** do seu aplicativo - para que você possa correlacionar eventos de rastreamento com solicitações.

- **Eventos personalizados e métricas** escrever você mesmo no código de cliente ou servidor hello, eventos de negócios tootrack como itens vendidos ou vitórias.
infraestrutura de saudação para seu aplicativo normalmente é composta de vários componentes – talvez uma máquina virtual, conta de armazenamento e rede virtual, ou um aplicativo web, banco de dados, servidor de banco de dados e 3º serviços de terceiros. Tais componentes não são vistos como entidades separadas, em vez disso, eles são mostrados como partes relacionadas e interdependentes de uma única entidade. Você deseja toodeploy, gerenciar e monitorá-los como um grupo. [Gerenciador de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) permite que você toowork com recursos de saudação em sua solução como um grupo.

Você pode implantar, atualizar ou excluir todos os recursos de saudação para sua solução em uma única operação coordenada. Usar um modelo para a implantação e esse modelo pode ser útil para ambientes diferentes, como teste, preparação e produção. Gerenciador de recursos fornece segurança, auditoria e marcação recursos toohelp gerenciar seus recursos após a implantação.

**benefícios de saudação do usando o Gerenciador de recursos**

O Gerenciador de Recursos fornece vários benefícios:

- Você pode implantar, gerenciar e monitorar todos os recursos de saudação para sua solução como um grupo, em vez de manipular esses recursos individualmente.

- Repetidamente, você pode implantar sua solução em todo o ciclo de vida de desenvolvimento hello e ter certeza de que seus recursos são implantados em um estado consistente.

- Você pode gerenciar sua infraestrutura por meio de modelos declarativos em vez de scripts.

- Você pode definir dependências de saudação entre os recursos, para que eles são implantados na ordem correta, Olá.

- Você pode aplicar tooall serviços de controle de acesso no seu grupo de recursos como controle de acesso baseado em função (RBAC) nativamente é integrado à plataforma de gerenciamento de saudação.

- Você pode aplicar marcas tooresources toologically organizar todos os recursos de saudação em sua assinatura.

- Você pode esclarecer a cobrança da sua organização exibindo custos para um grupo de recursos de compartilhamento Olá a mesma marca.

> [!Note]
> Gerenciador de recursos fornece um novo toodeploy de maneira e gerenciar suas soluções. Se você usou Olá modelo de implantação anterior e deseja toolearn sobre alterações hello, consulte [implantação clássica e implantação do Gerenciador de recursos de Noções básicas sobre](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre a segurança lendo alguns dos tópicos detalhados sobre segurança:

- [Auditoria e log](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [Crime cibernético](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [Design e segurança operacional](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [Criptografia](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [Gerenciamento de identidade e de acesso](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [Segurança de rede](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [Gerenciamento de ameaças](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
