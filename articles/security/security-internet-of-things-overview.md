---
title: aaaSecure sua Internet das coisas (IoT) no Azure | Microsoft Docs
description: " Os serviços de IoT (Internet das Coisas) do Azure oferecem uma ampla variedade de funcionalidades. Este artigo ajuda você a entender como toosecure suas soluções IoT no Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Visão geral da segurança da Internet das Coisas
Os serviços de IoT (Internet das Coisas) do Azure oferecem uma ampla variedade de funcionalidades. Esses serviços de nível corporativo permitem que você:

* Colete dados de dispositivos
* Analise fluxos de dados em movimento
* Armazene e consulte grandes conjuntos de dados
* Visualize dados históricos e em tempo real
* Realize a integração com sistemas de back-office

toodeliver esses recursos, o Azure IoT Suite pacotes juntos vários serviços do Azure com extensões personalizadas como soluções pré-configuradas. Essas soluções pré-configuradas são as implementações básicas dos padrões comuns de solução de IoT que ajudam a tooreduce Olá tempo você toodeliver suas soluções de IoT. Usando kits de desenvolvimento de software Olá IoT, você pode personalizar e estender essas soluções toomeet seus próprios requisitos. Você também pode usar essas soluções como exemplos ou modelos no desenvolvimento de novas soluções de IoT.

pacote do Azure IoT Olá é uma solução avançada para suas necessidades de IoT. No entanto, é imprescindível que suas soluções IoT destinam-se com segurança em mente a partir do início da saudação. Devido ao número absoluto de saudação de dispositivos IoT, qualquer incidente de segurança pode se tornar rapidamente um evento generalizado com consequências significativas.

toohelp você entender como toosecure suas soluções IoT, temos Olá informações a seguir.

## <a name="security-architecture"></a>Arquitetura de segurança
Durante a criação de um sistema, é importante toounderstand ameaças em potencial Olá toothat sistema e adicionar defesas apropriadas da mesma forma, como sistema de saudação é desenvolvido e projetado. É importante toodesign Olá produto a partir do início da saudação pensando na segurança porque a entender como um invasor pode ser capaz de toocompromise um sistema de ajuda a certificar-se de que as atenuações apropriadas estejam no local de início de saudação.

Você pode aprender sobre a arquitetura de segurança da IoT lendo o artigo [Arquitetura de segurança da Internet das Coisas](../iot-suite/iot-security-architecture.md).

Este artigo aborda Olá seguintes tópicos:

* [A segurança começa com um modelo de risco](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [Segurança na IoT](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Saudação de modelagem de ameaça arquitetura de referência de IoT do Azure](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Segurança de saudação de plano de fundo para cima
Olá IoT representa exclusivo segurança, privacidade e conformidade desafios toobusinesses em todo o mundo. Ao contrário da tecnologia tradicional cyber onde esses problemas giram em torno de software e como ele é implementado, IoT aborda o que acontece quando Olá cibernéticos e mundos físico Olá convergirem. Proteger soluções IoT requer garantindo provisionamento seguro de dispositivos, a conectividade segura entre esses dispositivos e a nuvem hello e a proteção de dados seguros na nuvem Olá durante o processamento e armazenamento. No entanto, trabalhando contra essa funcionalidade estão os dispositivos com recursos limitados, a distribuição geográfica das implantações e vários dispositivos em uma solução.

Você pode aprender como toohandle segurança nessas áreas lendo [segurança de Internet das coisas de saudação de plano de fundo](../iot-suite/securing-iot-ground-up.md).

Olá artigo Olá seguintes tópicos:

* [Infraestrutura segura de saudação de plano de fundo para cima](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure - infraestrutura segura da IoT para os seus negócios](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>Práticas Recomendadas
Proteger uma infraestrutura de IoT requer uma estratégia de segurança em camadas rigorosa. Da proteção de dados na nuvem hello, proteger a integridade de dados em trânsito pela Olá internet pública, dispositivos de provisionamento de toosecurely, cada camada cria maior garantia de segurança de Olá infra-estrutura geral.

Você pode aprender sobre as práticas recomendadas de segurança da Internet das Coisas lendo o artigo [Práticas recomendadas de segurança de Internet das Coisas](../iot-suite/iot-security-best-practices.md).

Olá artigo Olá seguintes tópicos:

* [Fabricante/integrador de hardware de IoT](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [Desenvolvedor de soluções IoT](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [Implantador de soluções IoT](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [Operador de solução IoT](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
