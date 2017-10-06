---
title: "aaaWhat é o Azure Key Vault? | Microsoft Docs"
description: "O Cofre da Chave do Azure ajuda a proteger chaves criptográficas e segredos usados por aplicativos e serviços em nuvem. Usando o Cofre da Chave do Azure, os clientes podem criptografar chaves e segredos (como chaves de autenticação, chaves de conta de armazenamento, chaves de criptografia de dados, arquivos .PFX e senhas) usando chaves que são protegidas por HSMs (módulos de segurança de hardware)."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>O que é o Cofre da Chave do Azure?
O Cofre da Chave do Azure está disponível na maioria das regiões. Para obter mais informações, consulte Olá [página de preços do Cofre de chaves](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introdução
O Cofre da Chave do Azure ajuda a proteger chaves criptográficas e segredos usados por aplicativos e serviços em nuvem. Usando o Cofre de Chaves, você pode criptografar chaves e segredos (como chaves de autenticação, chaves de conta de armazenamento, chaves de criptografia de dados, arquivos .PFX e senhas) usando chaves que são protegidas por HSMs (módulos de segurança de hardware). Para garantia extra, você pode importar ou gerar chaves em HSMs. Se você escolher toodo processos, Microsoft suas chaves de FIPS 140-2 nível 2 HSMs validados (hardware e firmware).  

Cofre de chaves simplifica o processo de gerenciamento de chaves hello e permite que você controle toomaintain de chaves que acessam e criptografar os dados. Os desenvolvedores podem criar chaves para desenvolvimento e teste em minutos e, em seguida, perfeitamente migrá-los tooproduction chaves. Os administradores de segurança podem conceder (e revogar) tookeys de permissão, conforme necessário.

Saudação de uso toobetter tabela a seguir entender como o Cofre de chaves pode ajudá toomeet necessidades de saudação de desenvolvedores e administradores de segurança.

| Função | Problema declarado | Solucionado pelo Cofre da Chave do Azure |
| --- | --- | --- |
| Desenvolvedor de um aplicativo do Azure |"Desejo toowrite um aplicativo do Azure que usa chaves de assinatura e criptografia, mas desejo toobe essas chaves externas de meu aplicativo para que a solução de saudação é adequada para um aplicativo que é distribuído geograficamente. <br/><br/>Também desejo esses toobe chaves e segredos protegidos, sem a necessidade de código de saudação toowrite sozinho. Também desejo toobe essas chaves e segredos fácil para mim toouse de meus aplicativos, com um desempenho ideal." |√ As chaves são armazenadas em um cofre e invocadas pelo URI quando necessário.<br/><br/> √ As chaves são protegidas pelo Azure, usando módulos de segurança de hardware (HSMs), comprimentos da chave e algoritmos padrão da indústria.<br/><br/> √ Chaves são processadas em HSMs que residem no hello mesmo Datacenter do Azure como aplicativos de saudação. Isso fornece melhor confiabilidade e latência reduzida se chaves Olá residem em um local separado, como no local. |
| Desenvolvedor de SaaS (software como serviço) |"Não quero responsabilidade de responsabilidade ou potencial Olá para segredos e chaves de locatário meus clientes. <br/><br/>Desejo Olá clientes tooown e gerenciar suas chaves para que possam concentrar-se sobre o que fazer melhor, que está fornecendo os recursos de software principal hello." |√ Os clientes podem importar suas próprias chaves para o Azure e gerenciá-las. Quando um aplicativo de SaaS precisa de operações criptográficas tooperform usando chaves de seus clientes, o Cofre de chaves não essas operações em nome do aplicativo hello. aplicativo Hello não verá chaves clientes hello. |
| Diretor-chefe de segurança (CSO) |"Eu quero tooknow que os aplicativos são compatíveis com FIPS 140-2 nível 2 HSMs para gerenciamento de chave seguro. <br/><br/>Desejo toomake se minha organização está no controle Olá chave do ciclo de vida e pode monitorar o uso da chave. <br/><br/>E embora usamos vários serviços do Azure e recursos, desejo que as chaves de saudação toomanage em um único local no Azure." |√ Os HSMs têm certificação FIPS 140-2 Nível 2.<br/><br/>√ O Cofre de Chaves foi projetado para que a Microsoft não veja nem extraia suas chaves.<br/><br/>√ Registro em log quase em tempo real do uso da chave.<br/><br/>Cofre de saudação √ fornece uma única interface, independentemente de quantas cofres no Azure, quais regiões suporte e quais aplicativos usá-los. |

Qualquer pessoa com uma assinatura do Azure pode criar e usar cofres de chaves. Embora o Cofre da Chave beneficie desenvolvedores e administradores de segurança, ele pode ser implementado e gerenciado pelo administrador de uma organização que gerencie outros serviços do Azure para a organização. Por exemplo, esse administrador deve entrar com uma assinatura do Azure, crie um cofre para a organização de saudação em quais chaves toostore e ser responsável por tarefas operacionais, como:

* Criar ou importar uma chave ou segredo
* Revogar ou excluir uma chave ou segredo
* Autorizar usuários ou aplicativos tooaccess Olá Cofre de chaves, para que possam gerenciar ou usar suas chaves e segredos
* Configurar o uso de chaves (por exemplo, assinar ou criptografar)
* Monitorar o uso de chaves

Esse administrador deve fornecer aos desenvolvedores toocall URIs de seus aplicativos e fornecer o seu administrador de segurança com as informações de log de uso de chave. 

   ![Visão geral da o Cofre da Chave do Azure][1]

Os desenvolvedores também podem gerenciar chaves de saudação diretamente, por meio de APIs. Para obter mais informações, consulte [Olá guia do desenvolvedor do Cofre de chaves](key-vault-developers-guide.md).

## <a name="next-steps"></a>Próximas etapas
Para ver um tutorial de introdução para um administrador, consulte [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md).

Para saber mais sobre o log de uso do Cofre da Chave, confira [Log do Cofre da Chave do Azure](key-vault-logging.md).

Para obter mais informações sobre como usar as chaves e os segredos com o Cofre de Chaves do Azure, consulte [Sobre Chaves, Segredos e Certificados](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx).

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
