---
title: "aaaInternet das práticas recomendadas de segurança de coisas | Microsoft Docs"
description: "artigo Olá fornece uma lista de curadoria de Microsoft Internet das coisas práticas recomendadas e recomendações gerais."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Práticas recomendadas de segurança de Internet das Coisas
Infraestrutura de Internet das coisas (IoT) protegendo Olá é uma tarefa crítica para todas as pessoas envolvidas com soluções de IoT. Devido a saudação e o número de saudação de dispositivos envolvidos natureza distribuída desses dispositivos, o impacto de saudação um evento de segurança relacionadas toocompromise de milhões de dispositivos IoT não é simples e pode ter impacto generalizado.

Por esse motivo, a segurança do IoT precisa de uma abordagem de segurança detalhada. Dados necessidades toobe segura na nuvem hello e como ele se move sobre redes privadas e públicas. Métodos necessário toobe no lugar toosecurely provisionar Olá IoT próprios dispositivos. Cada camada do dispositivo, toonetwork, garantias de alta segurança toocloud necessidades de back-end.

Práticas recomendadas do IoT podem ser categorizadas de saudação de maneira a seguir:

* Fabricante ou integrador de hardware de IoT
* Desenvolvedor de soluções IoT
* Implantador de soluções IoT
* Operador de solução IoT

Este artigo resume as [Práticas recomendadas de segurança de Internet das Coisas](../iot-suite/iot-security-best-practices.md). Consulte o artigo toothat para obter mais informações.

## <a name="iot-hardware-manufacturer-or-integrator"></a>Fabricante ou integrador de hardware de IoT
Siga as práticas recomendadas de saudação abaixo se você for um fabricante de hardware IoT ou o integrador de hardware:

* **Definir o escopo de requisitos de hardware do toominimum**: design de hardware Olá deve incluir recursos mínimos necessários para a operação de hardware Olá e nada mais. 
* **Verifique o hardware invioláveis**: Criar mecanismos de violação física toodetect do hardware, como abrir tampa do dispositivo hello, removendo a parte do dispositivo hello, etc. 
* **Criar em hardware seguro**: se o [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permitir, crie recursos de segurança, como as funcionalidades de inicialização baseadas no armazenamento seguro e criptografado e no TPM (Trusted Platform Module).
* **Fazer atualizações de segurança**: a atualização de firmware durante o tempo de vida do dispositivo Olá é inevitável.

## <a name="iot-solution-developer"></a>Desenvolvedor de soluções IoT
Siga as práticas recomendadas de saudação abaixo se você for um desenvolvedor de solução de IoT:

* **Siga a metodologia de desenvolvimento de software seguro**: desenvolvimento de software seguro requer o aterramento pensar sobre segurança desde a criação de saudação do projeto Olá todos Olá maneira tooits implementação, teste e implantação.
* **Escolha o software de código aberto com cuidado**: software livre fornece uma oportunidade tooquickly desenvolver soluções.
* **Integrar com cuidado**: muitas das falhas de segurança de software Olá existem no limite de saudação de bibliotecas e APIs. 

## <a name="iot-solution-deployer"></a>Implantador de soluções IoT
Siga as práticas recomendadas de saudação abaixo se você for um implantador de solução de IoT:

* **Implantar o hardware com segurança**: IoT implantações podem exigir hardware toobe implantado em locais não seguros, como espaços públicos ou localidades sem supervisão.
* **Proteger as chaves de autenticação**: durante a implantação, cada dispositivo requer identificações de dispositivo e chaves de autenticação geradas pelo serviço de nuvem Olá associadas. Mantenha essas chaves fisicamente seguro mesmo após a implantação de saudação. Qualquer chave comprometida pode ser usado por um dispositivo mal-intencionado toomasquerade como um dispositivo existente.

## <a name="iot-solution-operator"></a>Operador de solução IoT
Siga as práticas recomendadas de saudação abaixo se você for um operador de solução de IoT:

* **Manter os sistemas de toodate**: Certifique-se de que todos os drivers de dispositivo e sistemas operacionais de dispositivos são versões mais recentes do toohello atualizado. 
* **Proteger contra atividades mal-intencionadas**: se o sistema operacional de saudação permitir, coloque recursos mais recentes de antivírus e antimalware Olá em cada sistema operacional do dispositivo. 
* **Auditoria com frequência**: auditoria IoT infraestrutura para problemas é essencial ao responder a incidentes toosecurity relacionadas à segurança.
* **Proteja fisicamente a infraestrutura de IoT Olá**: Olá pior IoT infraestrutura ataques de segurança são iniciadas usando o acesso físico toodevices.
* **Proteger as credenciais de nuvem**: credenciais de autenticação de nuvem usadas para configuração e operação de uma implantação de IoT são possivelmente acesso de toogain de maneira mais fácil hello e comprometer um sistema de IoT. 

