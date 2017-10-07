---
title: "Azure Active Directory B2C: Notas do desenvolvedor sobre o uso de políticas personalizadas | Microsoft Docs"
description: "Observações para os desenvolvedores sobre configuração e manutenção do B2C do Azure AD com políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Notas de versão para a versão prévia da política personalizada do Azure Active Directory B2C
Olá conjunto de recursos de política personalizada agora está disponível para avaliação em visualização pública para todos os Azure Active Directory B2C clientes (Azure AD B2C). Esse conjunto de recursos é destinado a desenvolvedores de identidade avançado criando soluções de identidade hello mais complexas.  

Atualmente, esse conjunto de recursos exige os desenvolvedores tooconfigure Olá identidade experiência Framework diretamente por meio da edição de arquivo XML. Esse método de configuração é poderoso e complexo. Os desenvolvedores de identidade usando Olá avançados Framework de experiência de identidade deve planejar tooinvest algum tempo para concluir o passo a passo e leitura de documentos de referência. 

## <a name="features-included-in-this-public-preview"></a>Recursos incluídos nesta versão prévia
Com hello novos recursos introduzidos na visualização pública hello, os desenvolvedores podem executar Olá tarefas a seguir:<br>

* Criar e carregar percursos do usuário de autenticação personalizada usando políticas personalizadas. 
   * Descrever percursos do usuário passo a passo como trocas entre provedores de declarações. 
   * Definir a ramificação condicional em percursos do usuário. 
* Integrar os serviços habilitados para API REST aos seus percursos do usuário de autenticação personalizada.  
* Adicione a federação com provedores de identidade que são compatíveis com hello OpenIDConnect padrão. <br>
* Adicione a federação com provedores de identidade que seguem o protocolo toohello SAML 2.0. 

## <a name="terms-of-hello-public-preview"></a>Termos de visualização pública Olá

* Recomendamos que você toouse Olá novos recursos para fins de avaliação.<br>
* Os novos recursos não se destinam ao uso em um ambiente de produção.<br>
* Contratos de nível de serviço (SLAs) não se aplicam a toohello novos recursos. <br>
* As solicitações de suporte podem ser arquivadas por meio dos canais de suporte normais. <br>
* Não há nenhuma data prometida para disponibilidade geral.<br>
* Nosso critério e por qualquer motivo, Microsoft pode sinalizar e rejeitar ou restringir cenários e Jornadas de usuário que excedem o escopo de saudação do hello Azure AD B2C produto compromisso tooserve como uma plataforma de gerenciamento (CIAM) de identidade e acesso de cliente.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>Responsabilidades dos desenvolvedores de conjunto de recursos de política personalizada
Configuração da política manual concede acesso de nível inferior toohello subjacente a plataforma do Azure AD B2C e resulta na criação de saudação de uma estrutura de relação de confiança exclusivo e totalmente personalizável. As possíveis permutações de provedores de identidade personalizado, relações de confiança, a integração com serviços externos e fluxos de trabalho passo a passo coloca demandas maiores no Olá avançado desenvolvedores consumi-las.

toofully vantagem da visualização pública do hello, sugerimos que os desenvolvedores utilizando o conjunto de recursos de política personalizada do hello aderem toohello diretrizes a seguir:
* Familiarize-se com o idioma de configuração de saudação do hello mecanismo de experiência de identidade e gerenciamento de chave/segredos.
* Apropriar-se de cenários e de integrações personalizadas.
* Executar testes de cenário metódicos.
* Siga as práticas recomendadas de desenvolvimento/preparo de software com no mínimo um ambiente de desenvolvimento e teste um ambiente de produção.
* Se mantenha informado sobre novos desenvolvimentos de provedores de identidade hello e integrar com os serviços. Por exemplo, manter controle das alterações no segredos e do serviço de toohello programado e alterações.
* Configurar o monitoramento ativo e monitorar a capacidade de resposta de saudação de ambientes de produção.
* Manter os endereços de email de contato atuais e permanecer emails de site live equipe Microsoft toohello responsivo.
* Agir em tempo hábil quando toodo aconselhado Olá isso, a equipe do Microsoft live-site. 


>[!NOTE]
>Esses recursos eventualmente podem ser incluídos nas políticas internas do AD do Azure, tornando-os desenvolvedores de tooall mais acessíveis.

## <a name="next-steps"></a>Próximas etapas
[Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).
