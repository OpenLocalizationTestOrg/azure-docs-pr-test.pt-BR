---
title: "implantações de PaaS aaaSecuring | Microsoft Docs"
description: " Entender as vantagens de segurança de saudação do PaaS em comparação com outros modelos de serviço de nuvem e aprenda as práticas recomendadas para proteger a sua implantação PaaS do Azure. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>Proteção de implantações de PaaS

Este artigo fornece informações que ajudam você a:

- Entender as vantagens de segurança de saudação de hospedagem de aplicativos na nuvem Olá
- Avaliar as vantagens de segurança de saudação da plataforma como um serviço (PaaS) em comparação com outros modelos de serviço de nuvem
- Alterar o foco de segurança de uma abordagem de segurança de perímetro centrada em identidade tooan centrados em rede
- Implementar as recomendações de práticas recomendadas de segurança de PaaS gerais

## <a name="cloud-security-advantages"></a>Vantagens da segurança na nuvem
Há toobeing de vantagens de segurança na nuvem hello. Em um ambiente local, as organizações que provavelmente têm responsabilidades não atendidas e tooinvest de recursos limitados disponíveis em segurança, que cria um ambiente em que os invasores são tooexploit capaz de vulnerabilidades em todas as camadas.

![Vantagens de segurança da era da nuvem][1]

As organizações é tooimprove capaz de sua detecção de ameaças e tempos de resposta usando os recursos de segurança baseado em nuvem e inteligência de nuvem do provedor.  Pelo provedor de nuvem toohello responsabilidades de mudança, as organizações podem obter mais cobertura de segurança, que permite que eles tooreallocate os recursos de segurança e as prioridades de negócios do orçamento tooother.

## <a name="division-of-responsibility"></a>Divisão de responsabilidade
É importante toounderstand divisão de saudação de responsabilidade entre você e a Microsoft. No local, você possui a pilha inteira Olá mas à medida que você move nuvem toohello algumas responsabilidades transferir tooMicrosoft. Olá matriz de responsabilidade a seguir mostra áreas de saudação da pilha de saudação em uma implantação de SaaS, PaaS e IaaS que você é responsável por e Microsoft é responsável por.

![Zonas de responsabilidade][2]

Para todos os tipos de implantação de nuvem, você possui seus dados e identidades. Você é responsável por proteger Olá segurança de dados e identidades, recursos locais e Olá componentes de nuvem que você controle o (que varia por tipo de serviço).

Responsabilidades são sempre retidas por você, independentemente do tipo de saudação de implantação, são:

- Dados
- Pontos de extremidade
- Conta
- gerenciamento de acesso

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>Vantagens de segurança de um modelo de serviço de nuvem PaaS
Usando Olá mesma matriz de responsabilidade, vamos examinar vantagens de segurança de saudação de uma implantação PaaS do Azure versus local.

![Vantagens de segurança do PaaS][3]

Iniciando na parte inferior da saudação da pilha hello, infraestrutura física do hello, Microsoft reduz responsabilidades e riscos comuns. Saudação de nuvem da Microsoft é monitorada continuamente pela Microsoft, é tooattack de disco rígido. Não faz sentido para uma saudação de toopursue invasor nuvem da Microsoft como um destino. A menos que o invasor Olá tem muitos dinheiro e recursos, o invasor Olá é provavelmente toomove no destino tooanother.  

No meio de saudação da pilha hello, não há nenhuma diferença entre uma implantação PaaS e local. A camada de aplicativo hello e camada de gerenciamento de acesso e conta Olá, você tem riscos semelhantes. Olá próxima etapas seção deste artigo, vamos conduzi-lo toobest práticas para eliminar ou minimizar esses riscos.

Na parte superior de saudação da pilha hello, controle de dados e gerenciamento de direitos, você assume um risco que pode ser reduzido com o gerenciamento de chaves. (O gerenciamento de chaves é abordado nas práticas recomendadas.) Enquanto o gerenciamento de chaves é responsabilidade do adicional, você tem áreas em uma implantação PaaS que você não tem mais toomanage para que você pode alterar o gerenciamento de tookey de recursos.

Olá plataforma Azure também fornece proteção forte de DDoS usando diversas tecnologias baseadas em rede. No entanto, todos os tipos de métodos de proteção DDoS baseados em rede tem seus limites em uma base por link e por datacenter. toohelp evitar o impacto de saudação de ataques de DDoS grandes, você pode tirar proveito do recurso de nuvem do Azure core de permitir tooquickly e automaticamente toodefend contra ataques de DDoS em expansão. Veremos mais detalhes sobre como você pode fazer isso Olá práticas artigos recomendado.

## <a name="modernizing-hello-defenders-mindset"></a>Mentalidade do modernizar Olá defender
Implantações de PaaS vêm uma mudança na sua toosecurity abordagem geral. Deslocamento da necessidade toocontrol tudo o que você mesmo toosharing responsabilidade com a Microsoft.

Outra diferença significativa entre PaaS e implantações tradicionais locais, é uma nova exibição do que define o perímetro de segurança principal hello. Historicamente, perímetro de segurança local primário Olá foi sua rede mais locais e na segurança designs use Olá rede como seu dinâmico de segurança principal. Para implantações de PaaS, melhor você é atendidas, considerando o perímetro de segurança principal identidade toobe hello.

## <a name="identity-as-hello-primary-security-perimeter"></a>Identidade como o perímetro de segurança principal Olá
Um dos cinco características essenciais Olá da computação em nuvem é amplo acesso à rede, que torna centrados em rede pensando menos relevantes. Olá objetivo grande parte da computação em nuvem é tooallow usuários tooaccess recursos, independentemente do local. Para a maioria dos usuários, seu local está acontecendo toobe em algum lugar Olá da Internet.

Olá figura a seguir mostra como o perímetro de segurança Olá deixou de ser um perímetro da rede perímetro tooan identidade. A segurança se torna menos sobre como se proteger sua rede e mais sobre como se proteger seus dados, bem como gerenciar a segurança de saudação de seus aplicativos e usuários. Olá principal diferença é que você deseja que o da empresa do toowhat mais segurança toopush tooyour importantes.

![Identidade como novo perímetro de segurança][4]

Inicialmente, os serviços de PaaS do Azure (por exemplo, funções Web e SQL do Azure) forneciam pouca ou nenhuma defesa de perímetro de rede tradicional. Ele foi entendido que a finalidade do elemento Olá era toohello toobe exposto à Internet (função web) e que a autenticação fornece o perímetro de novo hello (por exemplo, o BLOB ou o SQL Azure).

Práticas recomendadas de segurança modernos presumem que adversário saudação tiver sido violado perímetro da rede hello. Portanto, práticas recomendadas de defesa modernos moveu tooidentity. As organizações devem estabelecer um perímetro de segurança com base em identidade com forte higiene de autenticação e autorização (práticas recomendadas).

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Recomendações para gerenciar o perímetro de identidade Olá

Princípios e padrões para o perímetro da rede Olá estão disponíveis por décadas. Por outro lado, setor Olá tem relativamente menos experiência com o uso de identidade como o perímetro de segurança principal hello. Dito isso, podemos acumulados suficiente tooprovide experiência algumas recomendações gerais comprovadas no campo hello e aplicar tooalmost todos os serviços de PaaS.

a seguir Olá resume uma toomanaging de abordagem de práticas recomendada gerais seu perímetro de identidade.

- **Não perca seu chaves ou as credenciais** proteção de chaves e credenciais é essencial toosecure implantações de PaaS. Perder chaves e credenciais é um problema comum. É uma ótima solução toouse uma solução centralizada onde as chaves e segredos podem ser armazenados em módulos de segurança de hardware (HSM). O Azure fornece um HSM na nuvem Olá com [Azure Key Vault](../key-vault/key-vault-whatis.md).
- **Não coloque as credenciais e outros segredos no código-fonte ou GitHub** Olá somente pior coisa de perder suas chaves e credenciais é fazer com que uma pessoa não autorizada obter acessar toothem. Os invasores são tootake capaz de aproveitar as chaves toofind de tecnologias de bot e segredos armazenados em repositórios de código, como GitHub. Não coloque a chave e segredos nesses repositórios de código-fonte públicos.
- **Proteja suas interfaces de gerenciamento de VM nos serviços de PaaS e IaaS híbridos** os serviços de IaaS e PaaS são executados em VMs (máquinas virtuais). Dependendo do tipo de saudação do serviço, várias interfaces de gerenciamento estão disponíveis que permitem que você tooremote gerenciar essas VMs diretamente. Protocolos de gerenciamento remoto, como o [protocolo SSH (Secure Shell)](https://en.wikipedia.org/wiki/Secure_Shell), o [protocolo RDP](https://support.microsoft.com/kb/186607) e o [PowerShell Remoto](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting), podem ser usados. Em geral, é recomendável não habilitar o acesso remoto direto tooVMs de saudação da Internet. Se estiver disponível, você deverá usar abordagens alternativas como usar rede virtual privada em uma rede virtual do Azure. Se não houver abordagens alternativas disponíveis, certifique-se de usar senhas complexas e quando estiver disponível, a autenticação de dois fatores (como [Autenticação Multifator do Azure](../multi-factor-authentication/multi-factor-authentication.md)).
- **Use plataformas de autorização e autenticação fortes**

  - Use identidades federadas no Azure AD, em vez de repositórios de usuário personalizados. Quando você usar identidades federadas, é possível aproveitar uma abordagem baseada em plataforma e você delega o gerenciamento de saudação de parceiros de tooyour identidades autorizados. Uma abordagem de identidade federada é especialmente importante em cenários quando os funcionários são encerrados e que informações precisa toobe refletidas por meio de várias identidade e autorização sistemas.
  - Use os mecanismos de autenticação e autorização fornecidos da plataforma em vez de código personalizado. motivo de saudação é desenvolver o código de autenticação personalizada pode ser propenso a erros. A maioria dos desenvolvedores não é especialistas em segurança e toobe improvável atento sutilezas hello e mais recentes desenvolvimentos Olá na autenticação e autorização. O código comercial (por exemplo, da Microsoft) frequentemente é extensivamente revisado quanto à segurança.
  - Use a autenticação multifator. A autenticação multifator é hello atual padrão para autenticação e autorização, porque ela evita vulnerabilidades de segurança Olá inerentes em tipos de nome de usuário e senha de autenticação. Interfaces de gerenciamento do Azure (portal/remota do PowerShell) do acesso tooboth hello e toocustomer serviços voltados para devem ser criados e configurados toouse [Azure multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md).
  - Use protocolos de autenticação padrão, como OAuth2 e Kerberos. Esses protocolos foram extensivamente revisados em pares e provavelmente são implementados como parte das bibliotecas da plataforma para autenticação e autorização.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, nos concentramos nas vantagens de segurança de uma implantação de PaaS do Azure. Em seguida, aprenda as práticas recomendadas para proteger suas soluções móveis e Web de PaaS. Começaremos com o Serviço de Aplicativo do Azure, o Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure. Conforme os artigos sobre práticas recomendadas para outros serviços do Azure ficam disponíveis, links serão fornecidos nos Olá lista a seguir:

- [Serviço de Aplicativo do Azure](security-paas-applications-using-app-services.md)
- [Banco de Dados SQL do Azure e SQL Data Warehouse do Azure](security-paas-applications-using-sql.md)
- Armazenamento do Azure
- Cache REDIS do Azure
- Barramento de Serviço do Azure
- Firewalls de aplicativo Web

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
