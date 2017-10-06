---
title: "Sincronização do Azure AD Connect: conceitos técnicos | Microsoft Docs"
description: "Explica conceitos técnicos de saudação de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Sincronização do Azure AD Connect: conceitos técnicos
Este artigo é um resumo do tópico Olá [Entendendo a arquitetura de](active-directory-aadconnectsync-technical-concepts.md).

O Azure AD Connect Sync tem como base uma plataforma sólida de sincronização de metadiretório.
Olá seções a seguir apresentam conceitos Olá para sincronização de metadiretório.
Compilação com base em MIIS, ILM e FIM, hello Azure Active Directory Sync Services fornece Olá próxima plataforma para conectar fontes de toodata, sincronizar dados entre fontes de dados, bem como Olá provisionamento e desprovisionamento de identidades.

![Conceitos técnicos](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Olá seções a seguir fornece mais detalhes sobre Olá aspectos do serviço de sincronização do FIM da saudação a seguir:

* Conector
* Fluxo de atributos
* Espaço conector
* Metaverso
* Provisionamento

## <a name="connector"></a>Conector
módulos de código Hello são usada toocommunicate com um diretório conectado são chamados de conectores (anteriormente conhecidos como agentes de gerenciamento (MAs)).

Eles são instalados no computador Olá executando a sincronização do Azure AD Connect. conectores de saudação fornecem Olá capacidade sem agente tooconverse por meio de protocolos de sistema remoto em vez de depender da implantação de saudação de agentes especializados. Isso significa que o risco e tempos de implantação reduzidos, especialmente ao lidar com sistemas e aplicativos críticos.

Imagem Olá acima, o conector de Olá é sinônimo de espaço do conector Olá mas engloba todas as comunicações com o sistema externo hello.

Olá conector é responsável por todas as importam e exportar funcionalidade toohello sistema e libera os desenvolvedores da necessidade toounderstand como tooconnect tooeach sistema nativamente ao usar transformações de dados toocustomize provisionamento declarativo.

As importações e exportações só ocorrem quando programadas, permitindo ainda mais isolamento das mudanças que ocorrem no sistema hello, desde que as alterações não se propagam automaticamente toohello fonte de dados conectada. Além disso, os desenvolvedores também podem criar seus próprios conectores para conectar-se toovirtually qualquer fonte de dados.

## <a name="attribute-flow"></a>Fluxo de atributos
Olá metaverso é a exibição de saudação consolidada de todas as identidades ingressadas dos espaços conectores vizinhos. Na Figura Olá acima, o fluxo de atributos é representado por linhas com setas para fluxo de entrada e saída. O fluxo de atributos é o processo de saudação de cópia ou de transformação de dados de um sistema tooanother e todos os atributos fluxos (entrados ou saídos).

O fluxo de atributos ocorre entre Olá espaço do conector e Olá metaverso bidirecional quando operações de sincronização (completa ou delta) são agendado toorun.

O fluxo de atributos ocorre apenas quando essas sincronizações são executadas. Fluxos de atributos são definidos nas Regras de Sincronização. Eles podem ser entrada (ISR na imagem de saudação acima) ou saída (OSR na imagem de saudação acima).

## <a name="connected-system"></a>Sistema conectado
Sistema conectado (também conhecido como diretório conectado) se refere a toohello de sistema remoto do Azure AD Connect sincronização conectou tooand leitura e gravação tooand de dados de identidade do.

## <a name="connector-space"></a>Espaço conector
Cada fonte de dados conectada é representada como um subconjunto filtrado dos objetos de saudação e atributos no espaço do conector hello.
Isso permite toooperate de serviço de sincronização Olá localmente sem Olá necessidade toocontact Olá remoto do sistema durante a sincronização de objetos de saudação e restringe tooimports interação e exporta apenas.

Quando fonte de dados de saudação e conector Olá tem Olá capacidade tooprovide uma lista de alterações (uma importação de delta), em seguida, Olá eficiência operacional aumentará drasticamente como apenas as alterações desde o último polling de saudação do ciclo é trocadas. espaço do conector Olá isola a fonte de dados conectada Olá de alterações que se propagam automaticamente exigindo que agenda Olá conector importa e exporta. Este seguro adicionado concede a você tranquilidade durante o teste, visualiza ou confirma a próxima atualização de saudação.

## <a name="metaverse"></a>Metaverso
Olá metaverso é a exibição de saudação consolidada de todas as identidades ingressadas dos espaços conectores vizinhos.

Conforme as identidades são vinculadas e a autoridade é atribuída a vários atributos através de mapeamentos de fluxo de importação, o objeto do metaverso central Olá começa tooaggregate informações de diversos sistemas. Deste fluxo de atributo de objeto, os mapeamentos carregam toooutbound os sistemas de informações.

Objetos são criados quando um sistema autoritativo os projeta no metaverso hello. Assim que todas as conexões são removidas, o objeto do metaverso Olá é excluído.

Objetos no metaverso Olá não podem ser editados diretamente. Todos os dados no objeto Olá devem estar contribuindo através do fluxo de atributos. Olá metaverso mantém conectores persistentes com cada espaço do conector. Esses conectores não exigem reavaliação para cada execução de sincronização. Isso significa que sincronização do Azure AD Connect não tem objeto remoto correspondente de saudação toolocate cada vez. Isso evita a necessidade de saudação de agentes dispendiosos tooprevent alterações tooattributes que normalmente seriam responsáveis para correlacionar os objetos de saudação.

Ao descobrir novas fontes de dados que podem ter objetos pré-existentes que precisem toobe gerenciado, usos de sincronização do Azure AD Connect em um processo chamado de uma junção regra tooevaluate potenciais candidatos com os quais tooestablish um link.
Depois de saudação vínculo é estabelecido, essa avaliação não reincide e fluxo de atributo normal pode ocorrer entre fonte de dados remota conectada hello e Olá metaverso.

## <a name="provisioning"></a>Provisionamento
Quando uma fonte autoritativa projeta um novo objeto no metaverso Olá um novo objeto de espaço do conector pode ser criado em outro conector que representa uma fonte de dados conectada downstream.

Inerentemente, isso estabelece um vínculo e o fluxo de atributo pode prosseguir bidirecionalmente.

Sempre que uma regra determina que um novo objeto de espaço do conector deve toobe criado, ele é chamado de provisionamento. No entanto, porque essa operação só acontece no espaço do conector hello, ele não será transferida a fonte de dados conectada Olá até uma exportação é executada.

## <a name="additional-resources"></a>Recursos adicionais
* [Azure AD Connect Sync: personalizando opções de sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
