---
title: "aaaOverview de um cenário de recuperação de desastres do Oracle em seu ambiente do Azure | Microsoft Docs"
description: "Um cenário de recuperação de desastre do banco de dados Oracle Database 12c no ambiente do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Recuperação de desastre para um banco de dados Oracle Database 12c em um ambiente do Azure

## <a name="assumptions"></a>Suposições

- Você compreende o design dos ambientes do Oracle Data Guard e do Azure.


## <a name="goals"></a>Metas
- Design topologia hello e configuração que atendem aos seus requisitos de recuperação de desastres.

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>Cenário 1: Sites primário e de recuperação de desastre no Azure

Um cliente tem um Oracle de banco de dados conjunto de backup no site primário hello. Um site de recuperação de desastre está em uma região diferente. Prezado cliente usa o Oracle Data Guard para recuperação rápida entre esses sites. site primário Olá também tem um banco de dados secundário para emissão de relatórios e outros usos. 

### <a name="topology"></a>Topologia

Aqui está um resumo da saudação configuração do Azure:

- Dois sites (um site primário e um site de recuperação de desastre)
- Duas redes virtuais
- Dois bancos de dados Oracle com Data Guard (primário e em espera)
- Dois bancos de dados Oracle com Golden Gate ou Data Guard (somente site primário)
- Dois serviços de aplicativo, um primário e no site de saudação DR
- Um *conjunto de disponibilidade,* que é usada para o serviço de banco de dados e aplicativo no site primário Olá
- Um jumpbox em cada site, o que restringe o acesso a rede privada toohello e só permite entrar por um administrador
- Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN em sub-redes separadas
- O NSG imposto em sub-redes de aplicativo e do banco de dados

![Captura de tela da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>Cenário 2: Site primário local e site de recuperação de desastre no Azure

Um cliente tem uma configuração de banco de dados Oracle local (site primário). Um site de recuperação de desastre reside no Azure. O Oracle Data Guard é usado para recuperação rápida entre esses sites. site primário Olá também tem um banco de dados secundário para emissão de relatórios e outros usos. 

Há duas abordagens para essa configuração.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>Abordagem 1: A conexão direta entre local e o Azure, a necessidade de abrir as portas TCP no firewall Olá 

Não é recomendável conexões diretas porque eles expõem Olá toohello de portas TCP fora do mundo.

#### <a name="topology"></a>Topologia

A seguir está um resumo de hello a instalação do Azure:

- Um site de recuperação de desastre 
- Uma rede virtual
- Um banco de dados Oracle com Data Guard (ativo)
- Serviço de um aplicativo no site de saudação DR
- Um jumpbox, que restringe o acesso a rede privada toohello e só permite entrar por um administrador
- Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN em sub-redes separadas
- O NSG imposto em sub-redes de aplicativo e do banco de dados
- A porta TCP 1521 (ou uma porta definidos pelo usuário) de entrada de um tooallow de regra de política/NSG
- Uma NSG/regra de política toorestrict somente Olá IP endereço/endereços locais (banco de dados ou aplicativo) tooaccess Olá rede virtual

![Captura de tela da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>Método 2: VPN Site a site
A VPN site a site é uma abordagem melhor. Para saber mais sobre como configurar uma VPN, veja [Criar uma rede virtual com uma conexão VPN Site a Site usando a CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).

#### <a name="topology"></a>Topologia

A seguir está um resumo de hello a instalação do Azure:

- Um site de recuperação de desastre 
- Uma rede virtual 
- Um banco de dados Oracle com Data Guard (ativo)
- Serviço de um aplicativo no site de saudação DR
- Um jumpbox, que restringe o acesso a rede privada toohello e só permite entrar por um administrador
- Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN ficam em sub-redes separadas
- O NSG imposto em sub-redes de aplicativo e do banco de dados
- Conexão VPN site a site entre sites locais e o Azure

![Captura de tela da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>Leitura adicional

- [Projetar e implementar um banco de dados Oracle no Azure](oracle-design.md)
- [Configurar o Oracle Data Guard](configure-oracle-dataguard.md)
- [Configurar o Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Backup e recuperação do Oracle](oracle-backup-recovery.md)


## <a name="next-steps"></a>Próximas etapas

- [Tutorial: criar VMs altamente disponíveis](../../linux/create-cli-complete.md)
- [Explorar exemplos da CLI do Azure de implantação de VM](../../linux/cli-samples.md)
