---
title: "recursos de segurança de rede de dados pessoais de aaaProtect com o Azure | Microsoft Docs"
description: "Proteger dados pessoais usando os recursos de segurança de rede do Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a>Proteger dados pessoais com os recursos de segurança de rede: Gateway de Aplicativo do Azure e Grupos de Segurança de Rede

Este artigo fornece informações e procedimentos que ajudarão você a usar grupos de segurança de rede e Gateway de aplicativo do Azure tooprotect de dados pessoais.

Um elemento importante de privacidade de saudação do tooprotect de estratégia várias camadas de segurança dos dados pessoais é uma defesa contra explorações de vulnerabilidade comuns, como a injeção de SQL ou script entre sites. Manter o tráfego de rede indesejado fora da sua rede virtual do Azure ajuda a proteger contra potencial comprometimento de dados confidenciais e dá Microsoft Azure você ferramentas toohelp proteger seus dados contra invasores.

## <a name="scenario"></a>Cenário

Uma empresa cruzeiro grandes, com sede Olá dos Estados Unidos, está expandindo suas roteiros de toooffer operações Mediterrâneo hello, Adriatic e mares báltico, bem como Olá Britânicas. Em favor dos esforços, ela adquiriu vários menor cruzeiro linhas com base no Reino Unido Itália, Alemanha, Dinamarca e Olá

Olá empresa usa o Microsoft Azure toostore dados corporativos Olá de nuvem e executar aplicativos em máquinas virtuais que processar e acessar esses dados. Esses dados incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes. Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais. linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.

Os funcionários corporativos acesso Olá rede da empresa Olá escritórios remotos e agentes Olá mundo têm acessar toosome os recursos da empresa e usar aplicativos web hospedados em máquinas virtuais do Azure toointeract com ele.

## <a name="problem-statement"></a>Problema declarado

empresa Olá deve proteger a privacidade de saudação de clientes e dados pessoais de funcionários de invasores que exploram software vulnerabilidades toorun código mal-intencionado que pode expor dados pessoais armazenados ou usados por aplicativos de baseado em nuvem da empresa hello.

## <a name="company-goal"></a>Meta da empresa

tooensure de meta da empresa não autorizados pessoas Hello não pode acessar dados permanecer lá Explorando vulnerabilidades comuns e aplicativos de saudação e corporativas redes virtuais do Azure. 

## <a name="solutions"></a>Soluções

O Microsoft Azure fornece segurança toohelp mecanismos evitar tráfego não desejado de inserir as redes virtuais do Azure. O controle do tráfego de entrada e saída é feito tradicionalmente por firewalls. No Azure, você pode usar o hello Application Gateway com hello Firewall do aplicativo Web e grupos de segurança da rede (NSG), que atuam como um firewall distribuído simple. Essas ferramentas permitem que você toodetect e bloqueiam o tráfego de rede indesejado.

### <a name="application-gatewayweb-application-firewall"></a>Gateway de Aplicativo/Firewall do Aplicativo Web

Olá [Firewall do aplicativo Web](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) componente (WAF) de saudação [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protege os aplicativos web, que são destinos de ataques mal-intencionados que exploram comuns conhecidas de cada vez mais vulnerabilidades. Um WAF centralizado protege contra ataques da Web e simplifica o gerenciamento de segurança sem a necessidade de nenhuma alteração no aplicativo.

O WAF do Azure lida com várias categorias de ataque, incluindo injeção de SQL, script entre sites, violações de protocolo HTTP e anomalias, bots, rastreadores, scanners, erros de configuração comuns de aplicativo, Negação de Serviço HTTP e outros ataques comuns como injeção de comando, solicitação HTTP indesejada, separação de resposta HTTP e ataques de inclusão de arquivo remoto. 

Você pode criar um gateway de aplicativo com WAF ou adicionar WAF tooan existente application gateway. Em ambos os casos, o Gateway de Aplicativo do Azure exige sua própria sub-rede.

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a>Como fazer para criar um gateway de aplicativo com o WAF? 

toocreate um novo gateway de aplicativo com WAF habilitado, Olá a seguir:

1. Log em toohello portal do Azure em Olá **Favoritos** painel do portal de saudação, clique em **novo**

2. Em Olá **novo** folha, clique em **rede**.

3. Clique em **Gateway de Aplicativo**.

4. Navegue toohello portal do Azure, **clique em novo \> rede \> Application Gateway.**

   ![criando gateways de aplicativo](media/protect-netsec/app-gateway-01.png)

5. Em Olá **Noções básicas sobre** folha que aparece, digite os valores de saudação para Olá campos a seguir: nome, a camada (Standard ou WAF), tamanho da SKU (pequeno, médio ou grande), (2 para alta disponibilidade), de contagem de instâncias assinatura, o grupo de recursos, e Local.

6. Em Olá **configurações** folha que aparece sob **rede Virtual**, clique em **escolha uma rede virtual**. Esta etapa abre insira Olá escolha folha de rede virtual.

7. Clique em **criar novo** tooopen Olá **criar rede virtual** folha.

8. Digite hello valores a seguir: nome, o espaço de endereço, o nome da sub-rede, o intervalo de endereços de sub-rede. Clique em **OK**.

9. Em Olá **configurações** folha sob **configuração de IP de Frontend**, escolha o tipo de endereço IP hello.

10. Clique em **Escolher um endereço IP público** e, em seguida, **Criar novo.**

11. Aceite o valor padrão de saudação e, em seguida, clique em **Okey.**

12. Em Olá **configurações** folha sob **configuração de ouvinte**, selecione toouse HTTP ou HTTPS em **protocolo**. toouse HTTPS, é necessário um certificado.

13. Definir as configurações específicas de saudação WAF: **Firewall status** (**habilitado**) e **modo Firewall** (**prevenção**). Se você escolher **detecção** como modo de saudação, o tráfego somente é registrado.

14. Saudação de revisão **resumo** página e clique em **Okey**. Agora o gateway de aplicativo hello enfileirado e criação.

Depois que o gateway de aplicativo hello foi criado, poderá navegar tooit no portal de saudação e continuar a configuração do gateway de aplicativo hello.

![gateway de aplicativo criado](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a>Como adicionar o aplicativo existente do WAF tooan?

tooupdate um toosupport WAF existente do application gateway no modo de prevenção, Olá a seguir:

1. No portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**.

2. Clique Olá existente do Application Gateway em Olá **todos os recursos** folha. 
>[!NOTE]
Observação: Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir Olá nome em Olá filtro por nome... zona DNS do hello caixa tooeasily acesso.
3. Clique em **firewall do aplicativo Web** e atualizar as configurações de gateway de aplicativo hello: **atualizar tooWAF camada** (marcada), **Firewall status** (habilitado),  **Modo de firewall** (prevenção). Você também precisa tooconfigure Olá conjunto de regras e configure as regras desabilitadas.

Para obter mais informações sobre como toocreate um novo gateway de aplicativo com WAF e como tooadd WAF tooan existente gateway de aplicativo, consulte [criar um gateway de aplicativos com o firewall do aplicativo web usando o portal de saudação.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)

### <a name="network-security-groups"></a>Grupos de segurança de rede

Um [grupo de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contém uma lista de regras de segurança que permitem ou negam tooresources de tráfego de rede conectados muito[redes virtuais do Azure](https://docs.microsoft.com/azure/virtual-network/) (VNet). Os NSGs podem ser associados toosubnets ou VMs individuais. Quando um NSG está associado tooa sub-rede, regras de saudação aplicam tooall recursos toohello conectado sub-rede. O tráfego pode ser restringido ainda mais associando também tooa um NSG VM ou NIC.

Os NSGs contêm quatro propriedades: Nome, Região, Grupo de recursos e Regras.
>[!Note]
Embora um NSG existe em um grupo de recursos, pode ser associado tooresources em qualquer grupo de recursos, como recursos Olá faz parte da saudação mesma região do Azure Olá NSG.

As regras do NSG contêm nove propriedades: Nome, Protocolo (TCP, UDP ou \*, que inclui o ICMP, bem como o TCP e UDP), Intervalo de portas de origem, Intervalo de portas de destino, Prefixo do endereço de origem, Prefixo do endereço de destino, Direção (entrada ou saída), Prioridade (entre 100 e 4096) e Tipo de acesso (permitir ou negar). Todos os NSGs contêm um conjunto de regras padrão que pode ser excluído ou substituído pelas regras de saudação que você criar.

#### <a name="how-do-i-implement-nsgs"></a>Como fazer para implementar os NSGs?

Implementar os NSGs requer planejamento e há várias considerações de design, é necessário tootake em conta. Isso inclui os limites de número de saudação do NSGs por assinatura e regras por NSG; Design de rede virtual e sub-rede, regras especiais, o tráfego ICMP, isolamento de camadas com sub-redes, balanceadores de carga e muito mais.

Para obter mais diretrizes de planejamento e implementação dos NSGs e um cenário de implantação de exemplo, consulte [Filtrar o tráfego de rede com grupos de segurança de rede.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)

#### <a name="how-do-i-create-rules-in-an-nsg"></a>Como fazer para criar regras em um NSG?

toocreate regras em um NSG existente de entrada, Olá a seguir:

1. Clique em **Procurar** e, em seguida, em **Grupos de segurança de rede**.

2. Na lista de saudação do NSGs, clique em **NSG-front-end**e, em seguida, **regras de segurança de entrada.**

3. Na lista de saudação de regras de segurança de entrada, clique em **adicionar.**

4. Insira valores hello no hello campos a seguir: nome, prioridade, fonte, protocolo, origem de intervalo, destino, destino intervalo de portas e ação.

nova regra de saudação aparecerá Olá NSG após alguns segundos.

![regras de segurança de rede](media/protect-netsec/inbound-security.png)

Para obter mais instruções sobre como criar regras toocreate NSGs em sub-redes e associar um NSG uma sub-rede front-end e back-end, consulte [criar grupos de segurança de rede usando Olá portal do Azure.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)

## <a name="next-steps"></a>Próximas etapas

[Segurança de rede do Azure](https://azure.microsoft.com/blog/azure-network-security/)

[Melhores práticas de segurança de rede do Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[Obter informações sobre um grupo de segurança de rede](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[WAF (Firewall do aplicativo Web)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
