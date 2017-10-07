---
title: "versões do MFA aaaAzure e consumo planos | Microsoft Docs"
description: "Informações sobre cliente de autenticação multifator hello e métodos diferentes de saudação e versões disponíveis. Detalhes sobre cada plano de consumo"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>Como tooget autenticação multifator do Azure

Quando se trata de tooprotecting suas contas, verificação em duas etapas deve ser padrão em sua organização. Esse recurso é especialmente importante para contas administrativas que têm privilegiado tooresources de acesso. Por esse motivo, a Microsoft oferece duas etapas básicas verificação recursos tooOffice 365 e administradores do Azure. Se você deseja que os recursos de saudação tooupgrade para seus administradores ou estende o resto de toohello de verificação em duas etapas de seus usuários, você pode comprar o Azure multi-Factor Authentication. 

Este artigo aborda explica Olá diferença entre as versões de saudação oferecidos tooadministrators e hello versão completa do Azure MFA e especifica quais recursos estão disponíveis em cada um. Se você estiver pronto Olá toodeploy concluir a oferta do Azure MFA, Olá posteriores opções de implementação de capas de seções e como o Microsoft calcula o consumo.

>[!IMPORTANT]
>Este artigo destina toobe toohelp um guia que você entender Olá toobuy de maneiras diferentes do Azure multi-Factor Authentication. Para obter detalhes específicos sobre preços e faturamento, você sempre deve consultar toohello [página de preços do multi-Factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Versões disponíveis do Azure Multi-Factor Authentication

Olá tabela a seguir descreve as diferenças de saudação entre três versões de autenticação multifator:

| Versão | Descrição |
| --- | --- |
| Autenticação Multifator para Office 365 |Esta versão funciona exclusivamente com os aplicativos do Office 365 e é gerenciado no portal de saudação Office 365. Os administradores podem [proteger recursos do Office 365 com a verificação de duas etapas](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Esta versão faz parte de uma assinatura do Office 365. |
| Autenticação Multifator para administradores do Azure | Administradores globais do Azure podem habilitar a verificação em duas etapas para suas contas de administrador globais sem custo adicional.|
| Autenticação Multifator do Azure | Versão "completo" tooas geralmente chamado hello, autenticação multifator do Azure oferece conjunto mais rico de saudação de recursos. Ele fornece opções de configuração adicionais por meio de saudação [portal clássico do Azure](https://manage.windowsazure.com), relatórios avançados e suporte para uma variedade de locais e aplicativos em nuvem. Autenticação multifator do Azure está incluída no Azure Active Directory Premium (planos P1 e P2) e mobilidade corporativa + segurança (planos E3 e E5) e pode ser implantado em [na nuvem hello ou no local](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Comparação de recursos dasversões
Olá tabela a seguir fornece uma lista dos recursos de saudação que estão disponíveis no hello várias versões do Azure multi-Factor Authentication.

> [!NOTE]
> Essa tabela de comparação aborda os recursos de saudação que fazem parte de cada versão do multi-Factor Authentication. Se você tiver o serviço de autenticação multifator do Azure completo hello, alguns recursos podem não estar disponíveis dependendo se você usar [MFA na nuvem hello ou MFA local](multi-factor-authentication-get-started.md).


| Recurso | Autenticação Multifator para Office 365 | Autenticação Multifator para administradores do Azure | Autenticação Multifator do Azure |
| --- |:---:|:---:|:---:|
| Proteger contas de administrador com MFA |● |● (Apenas para contas de Administrador Global) |● |
| Aplicativos móveis como um fator secundário |● |● |● |
| Chamada telefônica como um fator secundário |● |● |● |
| SMS como um fator secundário |● |● |● |
| Senhas de aplicativos para clientes que não oferecem suporte a MFA |● |● |● |
| Controle do administrador sobre métodos de verificação |● |● |● |
| Modo PIN | | |● |
| Alerta de fraude | | |● |
| Relatórios de MFA | | |● |
| Desvio único | | |● |
| Saudações personalizadas para chamadas telefônicas | | |● |
| ID do chamador personalizado para chamadas telefônicas | | |● |
| IPs confiáveis | | |● |
| Lembrar MFA para dispositivos confiáveis |● |● |● |
| SDK de MFA | | |● (Exige o provedor de Autenticação Multifator e assinatura completa do Azure) |
| MFA para aplicativos locais | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>Como tooget autenticação multifator do Azure
Se você desejar Olá todas as funcionalidades oferecidas pelo Azure multi-Factor Authentication, há várias opções:

### <a name="option-1---mfa-licenses"></a>Opção 1 - Licenças MFA

Comprar licenças de Azure multi-Factor Authentication e atribuí-los tooyour usuários no Active Directory do Azure. 

Se você usar essa opção, você deve criar um provedor de autenticação multifator do Azure somente se você também precisa tooprovide verificacao para alguns usuários que não têm licenças. Caso contrário, você poderá ser cobrado duas vezes.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>Opção 2 - Licenças agrupadas que incluem MFA

Compre licenças que incluem autenticação multifator do Azure, como o Azure Active Directory Premium (P1 ou P2) ou Enterprise Mobility + Security (E3 ou E5) e atribuí-los tooyour usuários no Active Directory do Azure. 

Se você usar essa opção, você deve criar um provedor de autenticação multifator do Azure somente se você também precisa tooprovide verificacao para alguns usuários que não têm licenças. Caso contrário, você poderá ser cobrado duas vezes. 

### <a name="option-3---mfa-consumption-based-model"></a>Opção 3 - modelo baseado no consumo de MFA

Crie um Provedor do Azure Multi-Factor Authentication em uma assinatura do Azure. Provedores de MFA do Azure são recursos do Azure que são cobrados em relação a seu Enterprise Agreement, Azure compromisso monetário ou cartão de crédito, assim como todos os outros recursos do Azure. Esses provedores podem ser criados somente em assinaturas do Azure completo, sem limitação, assinaturas do Azure que tenha um 0 $ limite de gastos. As assinaturas limitadas são criadas quando você ativa licenças, como nas opções 1 e 2. 

Ao usar um Provedor de Autenticação Multifator do Azure, há dois modelos de uso disponíveis que são cobrados por meio de sua assinatura do Azure:  

1. **Por usuário** - para empresas que desejam verificacao tooenable para um número fixo de funcionários que precisam regularmente de autenticação. A cobrança por usuário é com base no número de saudação de usuários habilitados para MFA em seu locatário Azure AD e/ou o servidor Azure MFA. Se os usuários estão habilitados para o MFA no AD do Azure e o servidor Azure MFA e a sincronização de domínio (Azure AD Connect) está habilitada, podemos contar conjunto maior de saudação de usuários. Se a sincronização de domínio não estiver habilitada, então podemos contar soma Olá de todos os usuários habilitados para MFA no AD do Azure e o servidor Azure MFA. A cobrança é o sistema de comércio de toohello rateados e será relatado diariamente. 

  > [!NOTE]
  > Exemplo de cobrança 1: você tem 5.000 usuários habilitados para MFA hoje. Olá sistema MFA divide esse número, 31 e 161.29 usuários relatórios para esse dia. Amanhã habilita 15 mais usuários, para que Olá sistema MFA relatórios 161.77 usuários para esse dia. Por final Olá Olá ciclo de cobrança, o número total de saudação de usuários cobrado em relação a sua assinatura do Azure adiciona backup tooaround 5.000. 
  >
  > Cobrança exemplo 2: você tiver uma mistura de usuários com licenças e os usuários sem, para que você tenha um toomake do provedor do Azure MFA por usuário diferença hello. Há 4.500 licenças do Enterprise Mobility + Security em seu locatário, mas 5.000 usuários habilitados para MFA. Sua assinatura do Azure é cobrada por 500 usuários, rateada e considerada 16.13 usuários diariamente. 

2. **Por autenticação** - para empresas que desejam tooenable verificacao para um grande grupo de usuários que raramente precisam de autenticação. Cobrança baseia-se no número de saudação de solicitações de verificação em duas etapas recebidas pelo Olá serviço de nuvem do Azure MFA, independentemente dessas verificações de êxito ou são negadas. Este cobrança aparece em sua instrução de uso do Azure nos pacotes de 10 autenticações e é o sistema de comércio de toohello relatado diariamente. 

  > [!NOTE]
  > Exemplo de cobrança 3: atualmente, Olá serviço Azure MFA recebido 3,105 solicitações de verificação em duas etapas. Sua assinatura do Azure é cobrada por 310,5 pacotes de autenticação. 

É importante toonote podem ter licenças de Azure MFA, mas ainda obter cobrado por configuração com base no consumo. Se você configurar um provedor de MFA por autenticação do Azure, você será cobrado para cada solicitação de verificação em duas etapas, mesmo aquelas feitas por usuários com licenças. Se você configurar um provedor de MFA do Azure por usuário em um domínio que não esteja vinculado tooyour locatário do AD do Azure, você será cobrado por usuário habilitado, mesmo se os usuários possuem licenças no AD do Azure. 

## <a name="next-steps"></a>Próximas etapas

- Para obter mais detalhes sobre preços, veja [Preços do Azure MFA](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Escolha se toodeploy Azure MFA [na nuvem de saudação ou no local](multi-factor-authentication-get-started.md)
