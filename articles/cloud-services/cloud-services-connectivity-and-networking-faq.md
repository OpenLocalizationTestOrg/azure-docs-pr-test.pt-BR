---
title: "problemas de rede e aaaConnectivity para perguntas frequentes sobre serviços de nuvem do Azure do Microsoft | Microsoft Docs"
description: "Este artigo lista Olá perguntas frequentes sobre a conectividade e rede para serviços de nuvem do Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de rede e conectividade para Serviços de Nuvem do Azure: perguntas frequentes

Este artigo inclui perguntas frequentes sobre problemas de conectividade e rede para [Serviços de Nuvem do Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Você também pode consultar Olá [página de tamanho de VM de serviços de nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Eu não consigo reservar um IP em um serviço de nuvem de vários VIPs
Primeiro, verifique se essa instância de máquina virtual Olá que você está tentando tooreserve Olá IP para está ativada. Em segundo lugar, certifique-se de que você está usando IPs reservados para ambos Olá implantações de preparo e produção. **Não** alterar configurações de saudação enquanto implantação hello está sendo atualizado.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Como acesso a área de trabalho remota quando tenho um NSG?
Adicionar regras toohello NSG que permitam o tráfego em portas **3389** e **20000**.  A Área de Trabalho Remota usa a porta **3389**.  Instâncias de serviço de nuvem têm a carga balanceada, portanto diretamente, você não pode controlar quais tooconnect de instância para.  Olá *RemoteForwarder* e *RemoteAccess* agentes gerenciar o tráfego RDP e permitir Olá cliente toosend um cookie RDP e especifique um tooconnect instância individual para.  Olá *RemoteForwarder* e *RemoteAccess* agentes exigem essa porta **20000** aberto, que pode ser bloqueado se você tiver um NSG.

## <a name="can-i-ping-a-cloud-service"></a>Posso executar ping de um serviço de nuvem?

Não, não utilizando a saudação normal "ping" / protocolo ICMP. Olá protocolo ICMP não é permitido por meio do balanceador de carga do Azure hello.

tootest conectividade, é recomendável que você faça um ping de porta. Enquanto o Ping.exe utiliza ICMP, outras ferramentas, como PSPing, Nmap e telnet permitem tootest conectividade tooa porta TCP.

Para obter mais informações, consulte [usar pings de porta em vez de ICMP tootest conectividade de VM do Azure](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Como impedir a receber milhares de acessos de endereços IP desconhecidos que indicam algum tipo de ataque mal-intencionado toohello serviço em nuvem?
Azure implementa um tooprotect de segurança de rede multicamadas seus serviços de plataforma contra ataques de (DDoS) de negação de serviço distribuídos. Olá sistema de proteção DDoS Azure faz parte do processo de monitoramento contínuo do Azure, que seja aprimorado continuamente por meio de teste de penetração. Este sistema de proteção DDoS foi projetado toowithstand ataques não apenas da saudação fora, mas também de outros locatários do Azure. Para obter mais detalhes, consulte [Segurança de Rede do Microsoft Azure](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

Você também pode criar um bloco de tooselectively de tarefa de inicialização alguns endereços IP específicos. Para obter mais informações, consulte [Bloquear um endereço IP específico](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Quando tento instância de serviço de nuvem tooRDP toomy, recebo a mensagem de saudação, "conta de usuário de saudação expirou."
Você pode receber a mensagem de erro hello "Esta conta de usuário expirou" quando você ignorar a data de expiração de saudação configurado nas configurações de RDP. Você pode alterar a data de expiração de saudação do portal Olá seguindo estas etapas:
1. Faça logon no toohello (https://manage.windowsazure.com) do Console de gerenciamento do Azure, navegue tooyour serviço de nuvem e selecione Olá **configurar** guia.
2. Selecione **Remoto**.
3. Alterar hello "Expira em" data e, em seguida, salvar a configuração de saudação.

Agora, você deve ser capaz de tooRDP tooyour máquina.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Por que o Balanceador de Carga não está balanceamento o tráfego uniformemente?
Para obter informações sobre como funciona o balanceador de carga interno, consulte [Novo modo de distribuição do Azure Load Balancer](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).

algoritmo de distribuição de saudação usado é uma tupla 5 (fonte de IP, porta de origem, IP de destino, porta de destino, o tipo de protocolo) servidores de tooavailable toomap tráfego de hash. Ele fornece permanência somente dentro de uma sessão de transporte. Pacotes em Olá mesma sessão TCP ou UDP será direcionado toohello instância mesmo datacenter IP (DIP) por trás do ponto de extremidade de balanceamento de carga de saudação. Quando o cliente Olá fecha e reabre a conexão de saudação ou inicia uma nova sessão de saudação mesmo IP de origem, porta de origem Olá altera e faz com que Olá tráfego toogo tooa DIP ponto de extremidade diferente.
