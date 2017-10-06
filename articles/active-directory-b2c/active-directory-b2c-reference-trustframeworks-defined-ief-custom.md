---
title: "Azure Active Directory B2C: referência – estruturas confiáveis | Microsoft Docs"
description: "Um tópico sobre políticas personalizadas do Azure Active Directory B2C e hello Framework de experiência de identidade"
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
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Definir estruturas confiáveis com a Estrutura de Experiência de Identidade do Azure AD B2C

B2C de diretório ativo do Azure (Azure AD B2C) políticas personalizadas que usam Olá identidade experiência Framework fornecem a sua organização com um serviço centralizado. Esse serviço reduz a complexidade de saudação da federação de identidade em uma grande comunidade de interesse. complexidade de saudação é reduzido tooa relação de confiança única e uma troca de metadados.

Políticas personalizadas do Azure AD B2C que usam Olá identidade experiência Framework tooenable você tooanswer Olá seguintes perguntas:

- Quais são Olá legal, segurança, privacidade e políticas de proteção de dados que devem ser seguidas?
- Quem são os contatos hello e quais são os processos de saudação para se tornar um participante reconhecido?
- Quem são Olá reconhecido provedores de informações de identidade (também conhecido como "provedores de declarações") e o que eles oferecem?
- Quem são Olá reconhecido terceiras partes confiáveis (e, opcionalmente, o que exige)?
- Quais são Olá técnica "no fio hello" requisitos de interoperabilidade para participantes?
- Quais são as regras de "runtime" operacionais de saudação que devem ser aplicadas para a troca de informações de identidade digital?

criar uma tooanswer todas essas perguntas, Azure AD B2C políticas personalizadas que usam Olá uso da estrutura de experiência de identidade Olá Framework confiar (TF). Vamos considerar esse constructo e o que ele oferece.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Entender a base de gerenciamento de estrutura de relação de confiança e a federação Olá

Olá Framework confiar é uma especificação escrita de saudação identidade, segurança, privacidade e dados políticas de proteção toowhich participantes em uma comunidade de interesse devem estar em conformidade.

A identidade federada fornece uma base para alcançar a garantia de identidade do usuário final em escala de Internet. Delegando partes de toothird de gerenciamento de identidade, uma única identidade digital de um usuário final pode ser reutilizada com várias partes confiáveis.  

Garantia de identidade requer que os provedores de identidade (IdPs) e provedores de atributo (AtPs) obedeçam toospecific segurança, privacidade e diretivas operacionais e práticas recomendadas.  Se eles não podem executar inspeções diretas, terceiras partes confiáveis (RPs) deve desenvolver relações de confiança com hello IdPs e AtPs escolhem toowork com.  

Conforme aumenta Olá número de consumidores e provedores de informações de identidade digital, é difícil toocontinue de gerenciamento emparelhadas essas relações de confiança ou mesmo Olá emparelhada troca de metadados de técnicas de saudação que é necessário para a conectividade de rede .  Os hubs de federação só alcançaram sucesso limitado na solução desses problemas.

### <a name="what-a-trust-framework-specification-defines"></a>O que uma especificação de Estrutura Confiável define
TFs são linchpins de saudação do modelo de abrir identidade Exchange (OIX) de confiança Framework hello, onde cada comunidade de interesse é controlada por uma especificação de TF específica. Tal especificação TF define:

- **Olá métricas de segurança e privacidade para a comunidade de saudação de interesse com a definição de saudação de:**
    - níveis de saudação de garantia (LOA) que são oferecidos/necessário por participantes; Por exemplo, um conjunto ordenado de classificações de confiança autenticidade de saudação de informações de identidade digital.
    - níveis de saudação de proteção (LOP) que são oferecidos/necessário por participantes; Por exemplo, um conjunto ordenado de classificações de confiança para a proteção de saudação de informações de identidade digital que são manipuladas pelo participantes na comunidade de saudação de interesse.

- **Olá descrição das informações de identidade digital de saudação que tem oferecido/necessária por participantes**.

- **Olá diretivas técnicas para produção e o consumo de informações de identidade digital e, portanto, para medir LOA e LOP. Eles gravados políticas normalmente incluem hello categorias de políticas a seguir:**
    - Políticas de verificação de identidade, por exemplo: *Qual é o nível de avaliação das informações de uma pessoa?*
    - Políticas de segurança, por exemplo: *Qual é o nível de proteção de confidencialidade e integridade das informações?*
    - Políticas de privacidade, por exemplo: *Qual controle um usuário tem sobre PII (informações pessoais identificáveis)*?
    - Políticas de persistência, por exemplo: *Se um provedor interromper as operações, como funcionará a continuidade e a proteção de PII?*

- **perfis de técnicas de Olá para produção e o consumo de informações de identidade digital. Esses perfis incluem:**
    - Interfaces de escopo para as quais as informações de identidade digital estão disponíveis em um LOA específico.
    - Requisitos técnicos para a interoperabilidade durante a transmissão.

- **Olá descrições de saudação várias funções que os participantes na comunidade de saudação podem executar e Olá qualificações que são necessária toofulfill essas funções.**

Assim, uma especificação de TF controla como informações de identidade são trocadas entre os participantes de saudação da comunidade de saudação de interesse: terceiras partes confiáveis, identidade e provedores de atributo e verificadores de atributo.

Uma especificação de TF é um ou vários documentos que servem como uma referência para governança de saudação da comunidade de saudação de interesse que regula asserção hello e consumo de informações de identidade digital na comunidade de saudação. É um conjunto de políticas de documentados e procedimentos criados tooestablish confiança identidades digitais de saudação que são usados para transações on-line entre os membros de uma comunidade de interesse.  

Em outras palavras, uma especificação de TF define regras de saudação para a criação de um ecossistema de identidade federada viável para uma comunidade.

Atualmente há contrato generalizado no benefício Olá dessa abordagem. É claro que confiança especificações do framework, facilitando o desenvolvimento de saudação de ecossistemas de identidade digital com verificáveis características de segurança, segurança e privacidade, que significa que eles podem ser reutilizados em várias comunidades de interesse.

Por esse motivo, Azure AD B2C políticas personalizadas que usam Olá identidade experiência Framework usa especificação hello como base de saudação de sua representação de dados para uma interoperabilidade de toofacilitate TF.  

Políticas de AD B2C personalizado do Azure que aproveitam Olá identidade experiência Framework representam uma especificação de TF como uma combinação de dados humanos e legível por máquina. Algumas seções desse modelo (normalmente seções que são mais orientadas para governança) são representadas como faz referência a documentação de política segurança e privacidade de toopublished junto com hello relacionados procedimentos (se houver). Outras seções descrevem em detalhes Olá metadados e tempo de execução de regras de configuração que facilitam a automação operacional.

## <a name="understand-trust-framework-policies"></a>Entender as políticas de estrutura confiável

Em termos de implementação, Olá especificação TF consiste em um conjunto de políticas que permitem o controle completo sobre comportamentos de identidade e experiências.  Políticas personalizadas do Azure AD B2C que aproveitam Olá identidade experiência Framework habilitar você tooauthor e criar seu próprios TF por meio dessas políticas declarativas que pode definir e configurar:

- referência de documento Hello ou referências que definem o ecossistema de identidade federada Olá da comunidade de saudação que relaciona toohello TF. Eles são documentação de TF toohello links. Olá regras operacionais (predefinido) "runtime" ou Jornadas de usuário Olá que automatizam e/ou controlam exchange hello e o uso de declarações de saudação. Esses percursos do usuário são associados a um LOA (e um LOP). Portanto, uma política pode ter percursos do usuário com diversos LOAs (e LOPs).

- provedores de declarações de provedores de identidade e atributo Hello, ou hello, na comunidade de saudação de interesse e hello perfis técnicas de suporte com capacitação LOA/LOP do hello (fora de banda) que relaciona toothem.

- integração de saudação verificadores de atributo ou provedores de declarações.

- Olá terceiras partes confiáveis na comunidade de saudação (por inferência).

- Olá metadados para estabelecer comunicações de rede entre os participantes. Esses metadados, juntamente com os perfis de técnicas de hello, são usados durante uma transação tooplumb "no fio hello" interoperabilidade entre terceira parte confiável hello e outros participantes da comunidade.

- Olá conversão de protocolo, se houver (por exemplo, SAML, OAuth2, WS-Federation e OpenID Connect).

- requisitos de autenticação Hello.

- Olá multifator orquestração se houver.

- Um esquema compartilhado para todas as declarações de saudação que estão disponíveis e tooparticipants mapeamentos de uma comunidade de interesse.

- Saudação de todas as declarações de transformações, junto com a redução de dados possíveis Olá neste contexto, o intercâmbio de saudação toosustain e uso de declarações de saudação.

- saudação de associação e criptografia.

- Olá declarações de armazenamento.

### <a name="understand-claims"></a>Entender as declarações

> [!NOTE]
> Coletivamente, fazemos referência tooall Olá possíveis tipos de informações de identidade que podem ser trocadas como "declarações": declarações sobre credenciais de autenticação do usuário final, habilitação de identidade, dispositivos de comunicação, localização física, de identificação pessoal atributos e assim por diante.  
>
> Usamos Olá termo "declarações" – em vez de "atributos" – como em transações on-line, esses artefatos de dados não são fatos que podem ser verificados diretamente pelo Olá terceira parte confiável. Em vez disso, eles são asserções ou declarações sobre fatos para qual Olá terceira parte confiável deve desenvolver transação solicitado suficiente confiança toogrant saudação do usuário final.  
>
> Também usamos o termo hello "declarações" porque o Azure AD B2C políticas personalizadas que usam saudação do Framework de experiência de identidade são projetados toosimplify intercâmbio de saudação de todos os tipos de informações de identidade digital de forma consistente, independentemente de se Olá subjacente protocolo é definido para recuperação de atributo ou autenticação de usuário.  Da mesma forma, usamos o termo hello "provedores de declarações" toocollectively consulte tooidentity provedores, provedores de atributo e verificadores de atributo quando não queremos toodistinguish entre suas funções específicas.   

Assim, eles controlam como as informações de identidade são trocadas entre uma terceira parte confiável, identidade, provedores de atributos e verificadores de atributos. Elas controlam quais identidades e provedores de atributos são necessários para autenticação de uma terceira parte confiável. Eles devem ser considerados como uma DSL (Linguagem Específica de Domínio), ou seja, uma linguagem de computador especializada para um domínio do aplicativo específico com herança, instruções *if*, polimorfismo.

Essas políticas constituem uma parte legível por máquina Olá Olá TF construir as políticas personalizadas do Azure AD B2C aproveitando saudação do Framework de experiência de identidade. Eles incluem todos os detalhes operacionais hello, incluindo metadados provedores de declarações e perfis técnicos, definições de esquema de declarações, funções de transformação de declarações e Jornadas de usuário que são preenchidas no orchestration operacionais toofacilitate e automação.  

Eles são considerados toobe *documentos de vida* porque não há uma boa chance de que seu conteúdo será alterado ao longo do tempo sobre participantes ativos de saudação declarados nas políticas de saudação. Também há possibilidade de Olá Olá termos e condições sendo um participante podem ser alterado.  

Configuração de Federação e manutenção amplamente são simplificados por blindagem terceiras partes confiáveis do reconfigurações de confiança e a conectividade contínuas, como provedores de declarações diferentes/verificadores ingressar ou sair (representada pela comunidade de Olá) Olá conjunto de políticas.

A interoperabilidade é outro desafio significativo. Verificadores/provedores de declarações adicionais devem ser integrados, como partes confiáveis são toosupport improvável todos Olá protocolos necessários. Políticas personalizadas do Azure AD B2C resolver esse problema, dando suporte a protocolos padrão do setor e aplicando Jornadas de usuário específico tootranspose solicitações quando terceiras partes confiáveis e provedores de atributo não oferecem suporte a Olá mesmo protocolo.  

Jornadas de usuário incluem perfis de protocolo e metadados que são usado tooplumb "no fio hello" interoperabilidade entre terceira parte confiável hello e outros participantes. Também há regras de tempo de execução operacionais que são mensagens de solicitação/resposta de exchange tooidentity aplicada informações para impor a conformidade com políticas publicadas como parte da especificação de TF hello. Olá ideia Jornadas de usuário é chave toohello personalização da experiência do usuário de saudação. Ele também esclarece como o sistema Olá funciona no nível do protocolo de saudação.

Com essa base, portais e aplicativos de terceiros confiável podem, dependendo de seu contexto, invocar políticas personalizadas do Azure AD B2C que aproveite Olá identidade experiência Framework passando Olá nome de uma política específica e obter precisamente o comportamento de saudação e informações Exchange quiserem sem qualquer muss, exagere ou de risco.
