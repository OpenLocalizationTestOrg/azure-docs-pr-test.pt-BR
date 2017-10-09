---
title: aaaConfigure servidor Azure MFA para alta disponibilidade | Microsoft Docs
description: "Implante várias instâncias do Servidor de Autenticação Multifator do Azure em configurações que fornecem alta disponibilidade."
services: multi-factor-authentication
keywords: MFA do Azure,
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>Configurar o Servidor de Autenticação Multifator do Azure para alta disponibilidade

tooachieve alta disponibilidade com a implantação do Azure MFA de servidor, você precisa toodeploy vários servidores MFA. Esta seção fornece informações sobre um design com balanceamento de carga tooachieve seus destinos de alta disponibilidade na implantação de servidor do Azure MFS.

## <a name="mfa-server-overview"></a>Visão geral do Servidor do MFA

Olá arquitetura de serviço do servidor Azure MFA consiste em vários componentes, conforme mostrado no diagrama a seguir de saudação:

 ![Arquitetura do Servidor do MFA](./media/mfa-server-high-availability/mfa-ha-architecture.png)

Um servidor de MFA é um servidor do Windows que tenha hello Azure multi-Factor Authentication software instalado. instância de servidor MFA Olá deve ser ativada por Olá serviço MFA em toofunction do Azure. Mais de um Servidor do MFA pode ser instalado localmente.

Olá primeiro servidor MFA instalado é Olá servidor mestre de MFA durante a ativação por hello Azure MFA serviço por padrão. servidor MFA mestre de saudação tem uma cópia gravável do banco de dados de PhoneFactor.pfdata hello. As instalações posteriores de instâncias do Servidor do MFA são conhecidas como servidores subordinados. secundários MFA de saudação tem uma cópia replicada somente leitura do banco de dados de PhoneFactor.pfdata hello. Os servidores do MFA replicam informações usando a RPC (Chamada de Procedimento Remoto). Todos os servidores de MFA deve coletivamente ser ingressado no domínio ou autônomo tooreplicate informações.

MFA mestre e escravo servidores MFA para se comunicar com hello serviço MFA quando a autenticação de dois fatores é necessária. Por exemplo, quando um usuário tenta toogain aplicativos de tooan de acesso que requer autenticação de dois fatores, Olá usuário primeiro será autenticado por um provedor de identidade, como o Active Directory (AD).

Após a autenticação bem-sucedida com o AD, Olá servidor MFA comunicará Olá serviço MFA. Olá servidor MFA aguarda a notificação de saudação serviço MFA tooallow ou negar o aplicativo de toohello de acesso de usuário hello.

Se o servidor mestre do MFA Olá ficar offline, autenticações ainda podem ser processadas, mas as operações que exigem alterações toohello MFA banco de dados não podem ser processadas. (Exemplos: Olá a adição de usuários, autoatendimento mudanças de PIN e alterar as informações de usuário)

## <a name="deployment"></a>Implantação

Considere Olá pontos importantes para balanceamento de carga do Azure MFA Server e seus componentes relacionados a seguir.

* **Usando a alta disponibilidade do RADIUS tooachieve padrão**. Se estiver usando Servidores do MFA do Azure como servidores RADIUS, poderá configurar potencialmente um Servidor do MFA como um destino de autenticação primária RADIUS e outros Servidores do MFA do Azure como destinos de autenticação secundária. No entanto, essa alta disponibilidade do método tooachieve pode não ser prática porque você deve aguardar um toooccur de período de tempo limite quando a autenticação falha no destino de autenticação primária Olá antes de você pode ser autenticados em relação a autenticação secundária Olá destino. É mais eficiente tooload saldo Olá tráfego RADIUS entre cliente RADIUS de saudação e servidores RADIUS de saudação (nesse caso, hello Azure MFA servidores atuando como servidores RADIUS) para que você pode configurar clientes RADIUS de saudação com uma única URL, eles podem apontar para.
* **Necessário toomanually promover secundários MFA**. Se o servidor mestre de Azure MFA Olá ficar offline, hello Azure MFA servidores secundários continuam tooprocess MFA solicitações. No entanto, até que um servidor mestre do MFA estiver disponível, administradores não podem adicionar usuários ou modificar as configurações de MFA, e os usuários não podem fazer alterações usando o portal do usuário hello. Promover uma função de mestre de toohello do MFA subordinado sempre é um processo manual.
* **Separabilidade de componentes**. Olá servidor MFA do Azure consiste em vários componentes que podem ser instalados em Olá a mesma instância do servidor do Windows ou em instâncias diferentes. Esses componentes incluem hello Portal do usuário, o serviço Web aplicativos móveis e o adaptador ADFS de saudação (agente). Este Separabilidade torna possível toouse Olá Olá de toopublish Proxy de aplicativo Web Portal do usuário e servidor de Web do aplicativo móvel da rede de perímetro hello. Essa configuração adiciona toohello geral de segurança do seu design, conforme mostrado no diagrama a seguir de saudação. Olá MFA Portal do usuário e o servidor de Web do aplicativo móvel também podem ser implantados em configurações de balanceamento de carga de alta disponibilidade.

   ![Servidor do MFA com uma rede de perímetro](./media/mfa-server-high-availability/mfasecurity.png)

* **Senha única (OTP) no SMS (também conhecido como SMS unidirecional) requer o uso de saudação de sessões Autoadesivas se o tráfego de balanceamento de carga**. SMS unidirecional é uma opção de autenticação que faz com que os usuários o Olá Olá servidor MFA toosend uma mensagem de texto que contém uma OTP. usuário de Olá insere Olá OTP em uma saudação de toocomplete da janela de prompt desafio MFA. Se você Azure MFA servidores de balanceamento de carga, hello mesmo servidor que serviu a solicitação de autenticação inicial Olá deve ser Olá servidor que recebe uma mensagem OTP de saudação do usuário Olá; Se outro servidor MFA recebe Olá resposta OTP, o desafio de autenticação Olá falhará. Para obter mais informações, consulte [senha por SMS adicionados tooAzure servidor MFA](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server).
* **As implantações de balanceamento de carga de saudação Portal do usuário e o serviço Web aplicativos móveis requerem sessões Autoadesivas**. Se você balanceamento de carga Olá MFA Portal do usuário e saudação do serviço Web de aplicativo móvel, cada sessão precisa toostay em Olá mesmo servidor.

## <a name="high-availability-deployment"></a>Implantação de alta disponibilidade

Olá diagrama a seguir mostra uma implementação de balanceamento de carga de alta disponibilidade completa do Azure MFA e seus componentes, juntamente com o AD FS para referência.

 ![Implementação de HA do Servidor do MFA do Azure](./media/mfa-server-high-availability/mfa-ha-deployment.png)

Observe Olá itens para a área de saudação numerada de forma correspondente de saudação precede o diagrama a seguir.

1. Olá são dois servidores do Azure MFA (MFA1 e MFA2) (mfaapp.contoso.com) com balanceamento de carga e são toouse configurado um banco de dados de PhoneFactor.pfdata de saudação do tooreplicate (4443) de porta estática. Olá SDK do serviço Web está instalado em cada um de comunicação de tooenable do servidor MFA Olá pela porta TCP 443 com servidores do ADFS hello. servidores MFA de saudação são implantados em uma configuração de balanceamento de carga sem monitoração de estado. No entanto, se você quisesse toouse OTP no SMS, você deve usar o balanceamento de carga com monitoração de estado.
   ![Servidor do MFA do Azure – HA do servidor de aplicativos](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > Como o RPC usa portas dinâmicas, é recomendável não firewalls tooopen toohello o intervalo de portas dinâmicas RPC pode potencialmente usar. Se você tiver um firewall **entre** seus servidores de aplicativo de MFA, você deve configurar Olá servidor MFA toocommunicate em uma porta estática para Olá tráfego de replicação entre servidores mestre e subordinado e abra a porta no firewall. Você pode forçar a porta estática hello, criando um valor de Registro DWORD em ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` chamado ```Pfsvc_ncan_ip_tcp_port``` e definindo o valor de saudação tooan porta estática. Conexões sempre são iniciadas pelo mestre de toohello Olá subordinado servidores MFA, porta estática Olá só é necessário no mestre hello, mas desde que você pode promover um mestre de saudação toobe subordinado a qualquer momento, você deve definir a porta estática Olá em todos os servidores de MFA.

2. servidores de aplicativo do usuário MFA do Portal móvel Olá dois (MFA-UP-MAS1 e MFA-UP-MAS2) têm a carga balanceada em um **com monitoração de estado** configuração (mfa.contoso.com). Lembre-se de que as sessões Autoadesivas são um requisito para balanceamento de carga Olá MFA Portal do usuário e o serviço de aplicativo móvel.
   ![Servidor do MFA do Azure – HA do Portal do Usuário e do Serviço de Aplicativo Móvel](./media/mfa-server-high-availability/mfaportal.png)
3. farm de servidor ADFS Olá é carga balanceada e publicados toohello da Internet por meio de proxies do AD FS com balanceamento de carga na rede de perímetro hello. Cada servidor do AD FS usa Olá ADFS agente toocommunicate com hello Azure MFA servidores usando uma URL de única com balanceamento de carga (mfaapp.contoso.com) pela porta TCP 443.

## <a name="next-steps"></a>Próximas etapas

* [Instalar e configurar o Servidor do MFA do Azure](multi-factor-authentication-get-started-server.md)
