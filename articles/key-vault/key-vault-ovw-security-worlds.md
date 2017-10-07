---
ms.assetid: 
title: "mundos de segurança do Cofre de chaves aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Universos de segurança e limites geográficos do Azure Key Vault

O Azure Key Vault é um serviço multilocatário e usa um pool de HSMs (Módulos de Segurança de Hardware) em cada localização do Azure. 

Todos os HSMs nos locais do Azure da saudação mesma região geográfica compartilham Olá mesmo limite de criptografia (Thales mundo de segurança). Por exemplo, EUA Leste e Oeste dos EUA compartilhar Olá mundo de segurança mesmo porque elas pertencem a localização geográfica de toohello dos EUA. Da mesma forma, todos os locais do Azure no compartilhamento Japão Olá mundo de segurança mesmo e todos os locais do Azure na Austrália, Índia e assim por diante. 

## <a name="backup-and-restore-behavior"></a>Comportamento de backup e restauração

Um backup feito de uma chave de um cofre de chaves em um local do Azure pode ser restaurados tooa Cofre de chaves em outro local do Azure, desde que essas duas condições forem verdadeiras:

- Ambos hello Azure locais pertencem toohello mesmo local geográfico
- Cofre de chave Olá pertencer toohello mesma assinatura do Azure

Por exemplo, um backup feito por uma determinada assinatura de uma chave em um cofre de chaves no Oeste da Índia, só pode ser restaurado tooanother Cofre de chaves em Olá mesma assinatura e localização geográfica; Oeste da Índia, Índia Central ou Sul da Índia.

## <a name="regions-and-products"></a>Regiões e produtos

- [Regiões do Azure](https://azure.microsoft.com/regions/)
- [Produtos da Microsoft por região](https://azure.microsoft.com/regions/services/)

Regiões são mapeadas toosecurity mundos, mostrados como títulos principais nas tabelas de saudação:

Em produtos Olá pelo artigo da região, por exemplo, Olá **Américas** guia contém Leste EUA, centro dos EUA, oeste dos EUA todos os mapeamento toohello Américas região. 

>[!NOTE]
>Uma exceção é que US DOD LESTE e US DOD CENTRAL têm seus próprios mundos de segurança. 

Da mesma forma, em Olá **Europa** guia, Norte da Europa e Europa Ocidental são mapeados toohello região da Europa. Olá mesmo também ocorre em Olá **Ásia-Pacífico** guia.



