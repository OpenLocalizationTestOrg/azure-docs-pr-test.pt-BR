---
title: aaaHow tooLink tooAzure uma assinatura do Azure AD B2C | Microsoft Docs
description: "Guia passo a passo tooenable a cobrança de locatário do Azure AD B2C em uma assinatura do Azure."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Vinculando um toopay de locatário assinatura do Azure tooan B2C do Azure para encargos de uso

Encargos de uso contínuo do Azure Active Directory B2C (ou Azure AD B2C) são cobrada tooan assinatura do Azure. É necessário para Olá locatário administrador tooexplicitly link hello Azure AD B2C locatário tooan assinatura do Azure depois de criar o locatário Olá B2C em si.  Este link é obtido por meio da criação do Azure AD "B2C locatário" recurso no destino Olá assinatura do Azure. Vários locatários B2C podem ser vinculado tooa única assinatura do Azure junto com outros recursos do Azure (por exemplo, máquinas virtuais, armazenamento de dados, LogicApps)


> [!IMPORTANT]
> Olá informações mais recentes sobre o uso de cobrança e preços para B2C em Olá página a seguir: [preços do Azure AD B2C](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>Etapa 1 - Criar um locatário do Azure AD B2C
A criação do locatário do B2C deve ser concluída primeiro. Ignore esta etapa se você já tiver criado seu Locatário do B2C de destino. [Introdução ao Azure AD B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>Etapa 2: abrir o portal do Azure no hello locatário do AD do Azure que mostra a sua assinatura do Azure
Navegue toohello [portal do Azure](https://portal.azure.com). Alterne toohello locatário do AD do Azure que mostra Olá assinatura do Azure que você gostaria que toouse. Este locatário do AD do Azure é diferente do locatário do hello B2C. No hello portal do Azure, clique em nome da conta Olá direita superior de saudação do hello tooselect de painel Olá locatário do AD do Azure. Uma assinatura do Azure é tooproceed necessário. [Obter uma assinatura do Azure](https://account.windowsazure.com/signup?showCatalog=True)

![Alternando tooyour locatário do AD do Azure](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>Etapa 3 - Criar um recurso de locatário do B2C no Azure Marketplace
Abra o Marketplace clicando ícone do Marketplace hello, ou selecionando Olá verde "+" no canto superior esquerdo de saudação do painel de saudação.  Procurar e selecionar o Azure Active Directory B2C. Selecione Criar.

![Selecionar o Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![Pesquisar AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Olá recursos do Azure AD B2C criar diálogo abrange Olá parâmetros a seguir:

1. Locatário do AD B2C do Azure – selecione um locatário Azure AD B2C na lista suspensa de saudação.  Somente os locatários do Azure AD B2C qualificados são mostrados.  Locatários de B2C qualificados atendem estas condições: você é administrador global de saudação do locatário Olá B2C e locatário Olá B2C não está associado atualmente tooan assinatura do Azure

2. Nome de recurso AD B2C do Azure - é o nome de domínio de saudação de toomatch pré-selecionados de saudação B2C locatário

3. Assinatura – uma assinatura ativa do Azure no qual você é um administrador ou um coadministrador.  Vários locatários Azure AD B2C podem ser adicionados como tooone assinatura do Azure

4. Grupo de Recursos e local do Grupo de Recursos - esse artefato ajuda a organizar vários recursos do Azure.  Essa opção não afeta o local, o desempenho ou o status de cobrança do locatário do B2C

5. Fixar toodashboard para o locatário de tooyour B2C acesso mais fácil cobrança informações e hello configurações de locatário B2C ![criar B2C recurso](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>Etapa 4 - Gerenciar os recursos do Locatário do B2C (opcional)
Após a conclusão da implantação, um novo recurso de "B2C locatário" é criado no grupo de recursos de destino hello e relacionados a assinatura do Azure.  Você verá um novo recurso do tipo "Locatário do B2C" adicionado junto com outros recursos do Azure.

![Criar recurso do B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

Ao clicar em recursos de locatário Olá B2C, é possível
- Clique em informações de cobrança do tooreview de nome de assinatura. Consultar Cobrança e Uso.
- Clique em configurações do Azure AD B2C tooopen uma nova guia do navegador diretamente no locatário tooyour B2C folha de configurações
- Enviar uma solicitação de suporte
- Mover o tooanother de recursos de locatário B2C tooanother grupo de recursos ou assinatura Azure.  Essa opção altera a assinatura do Azure que receberá os encargos de uso.

![Configurações de Recursos do B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Problemas conhecidos
- Exclusão de locatário B2C. Se um locatário B2C é criado, excluídos e recriados com hello o mesmo nome de domínio, também exclua e crie novamente o recurso "Vinculação" Olá Olá mesmo nome de domínio.  Você encontrará isso "Vinculação" de recurso em "Todos os recursos" no locatário da assinatura de saudação pelo Olá portal do Azure.
- Restrições autoimpostas sobre o local do recurso regional.  Em casos raros, um usuário pode ter estabelecido uma restrição regional para a criação de recursos do Azure.  Essa restrição pode impedir a criação de saudação do hello Link entre uma assinatura do Azure e um locatário B2C. toomitigate, relaxe essa restrição.

## <a name="next-steps"></a>Próximas etapas
Quando essas etapas forem concluídas para cada um dos seus locatários do B2C, sua assinatura do Azure será cobrada de acordo com os detalhes do Azure Direct ou Enterprise Agreement.
- Examinar o uso e a cobrança selecionados para a assinatura do Azure
- Examine os relatórios de uso detalhadas do dia a dia usando Olá [API de relatórios de uso](active-directory-b2c-reference-usage-reporting-api.md)
