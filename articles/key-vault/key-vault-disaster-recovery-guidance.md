---
title: "toodo aaaWhat no evento de saudação de uma interrupção de serviço do Azure que afeta o Cofre de chaves do Azure | Microsoft Docs"
description: "Saiba quais toodo no evento de saudação de uma interrupção de serviço do Azure que afeta o Cofre de chaves do Azure."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Redundância e disponibilidade de Cofre de Chaves do Azure
Cofre de chaves do Azure apresenta várias camadas de redundância toomake se suas chaves e segredos permanecem disponíveis tooyour aplicativo mesmo se os componentes individuais do hello serviço falhar.

Olá conteúdo de seu Cofre de chaves é replicado dentro Olá regiões e tooa secundário, pelo menos, 150 milhas imediatamente, mas dentro de saudação mesmo Geografia. Isso mantém a alta durabilidade de seus segredos e chaves. Consulte Olá [Azure emparelhado regiões](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) documento para obter detalhes sobre os pares de região específica.

Se os componentes individuais no serviço de Cofre de chaves Olá falharem, componentes alternativos na região Olá etapa na tooserve seu toomake solicitação se não há nenhuma degradação de funcionalidade. Você não precisa tootake tootrigger qualquer ação isso. Ela ocorre automaticamente e será tooyou transparente.

No evento raro Olá que toda a uma região do Azure está disponível, Olá solicitações feitas de Cofre de chaves do Azure nessa região são roteadas automaticamente (*failover*) região secundária tooa. Quando a região primária Olá esteja disponível novamente, as solicitações são roteadas novamente (*falha volta*) região primária toohello. Novamente, não é necessário tootake qualquer ação porque isso ocorre automaticamente.

Há alguns toobe de advertências atento:

* Evento de saudação de um failover de região, levará alguns minutos para Olá serviço toofail. As solicitações feitas durante esse tempo podem falhar até a conclusão do failover de saudação.
* Após a conclusão de um failover, o cofre de chaves estará no modo somente leitura. As solicitações permitidas nesse modo são:
  * Listar cofres de chave
  * Obter propriedades de cofres de chave
  * Listar segredos
  * Obter segredos
  * Listar chaves
  * Obter (propriedades das) chaves
  * Criptografar
  * Descriptografar
  * Encapsular
  * Desencapsular
  * Verificar
  * Assinar
  * Backup
* Após o failback de um failover, todos os tipos de solicitação (ou seja, solicitações de leitura *e* de gravação) são disponibilizados.

