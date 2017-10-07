---
title: eventos de risco do Active Directory aaaAzure | Microsoft Docs
description: "Este tópico fornece uma visão geral detalhada do que são os eventos de risco."
services: active-directory
keywords: "proteção de identidade do azure active directory, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Eventos de risco do Azure Active Directory

maioria de saudação de levar violações de segurança colocar quando os invasores obterem o ambiente de tooan acesso pelo roubo de identidade do usuário. Descobrir identidades comprometidas não é uma tarefa fácil. Active Directory do Azure usa algoritmos e heurística toodetect suspeitas ações relacionadas tooyour contas de usuário de aprendizado de máquina adaptável. Cada ação suspeita detectada é armazenada em um registro chamado *evento de risco*.

Atualmente, o Azure Active Directory detecta seis tipos de eventos de risco:

- [Usuários com credenciais vazadas](#leaked-credentials) 
- [Entradas de endereços de IP anônimos](#sign-ins-from-anonymous-ip-addresses) 
- [Viagem impossível tooatypical locais](#impossible-travel-to-atypical-locations) 
- [Entradas de locais desconhecidos](#sign-in-from-unfamiliar-locations)
- [Entradas de dispositivos infectados](#sign-ins-from-infected-devices) 
- [Entradas de endereços de IP com atividade suspeita](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![Evento de risco](./media/active-directory-reporting-risk-events/91.png)

Este tópico fornece a você uma visão geral detalhada de quais eventos de risco e como você pode usá-los tooprotect suas identidades do AD do Azure.


## <a name="risk-event-types"></a>Tipos de evento de risco

propriedade de tipo de evento de risco Olá é que foi criado para um identificador para a ação de suspeita Olá um registro de evento de risco.  
Investimentos contínuos da Microsoft para o processo de detecção de saudação conduzir a:

- Precisão da detecção toohello aprimoramentos de eventos de risco existentes 
- Novos tipos de eventos de risco que serão adicionados em Olá futuras

### <a name="leaked-credentials"></a>Credenciais vazadas

Quando cibercriminosos comprometem válidas senhas de usuários legítimos, criminosos Olá geralmente compartilham essas credenciais. Geralmente, isso é feito por meio de postagem publicamente em sites da web ou colar escuros hello ou comerciais ou credenciais Olá Olá preto mercado de venda. Microsoft Hello vazadas credenciais de serviço adquire o nome de usuário / senha pares pelo monitoramento de sites da web público e escuro e trabalhando com:

- Pesquisadores
- Representantes legais
- Equipes de segurança da Microsoft
- Outras fontes confiáveis 

Quando o serviço de saudação adquire o nome de usuário / pares de senha, eles são verificados em relação a credenciais válidas atual de usuários do AAD. Quando uma correspondência é encontrada, isso significa que a senha do usuário foi comprometida e um *evento de risco de credenciais vazadas* é criado.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Entradas de endereços IP anônimos

Esse tipo de evento de risco identifica os usuários que entraram com êxito de um endereço IP que foi identificado como um endereço IP de proxy anônimo. Esses proxies são usados por pessoas que desejam toohide endereço IP do seu dispositivo e podem ser usadas com objetivos mal-intencionados.


### <a name="impossible-travel-tooatypical-locations"></a>Viagem impossível tooatypical locais

Esse tipo de evento de risco identifica duas entradas provenientes de locais geograficamente distantes, onde pelo menos um dos locais de saudação também pode ser atípico para usuário hello, fornecido ao comportamento anterior. Além disso, o tempo de saudação entre Olá duas entradas é menor do que o tempo de saudação que teria levado Olá usuário tootravel de saudação primeiro local toohello segundo, que indica que um usuário diferente está usando Olá mesmo credenciais. 

Esse algoritmo de aprendizado de máquina que ignora óbvio "*falsos positivos*" toohello viagem impossível condição, como locais regularmente usadas por outros usuários na organização hello e VPNs de contribuição.  sistema de saudação tem um período inicial de assimilação de 14 dias, durante o qual ele aprende o comportamento de logon do novo usuário.

### <a name="sign-in-from-unfamiliar-locations"></a>Entrada de locais desconhecidos

Esse tipo de evento de risco considera após entrar locais (IP, Latitude / Longitude e ASN) toodetermine locais de novo / desconhecidos. sistema de saudação armazena informações sobre locais anteriores, usados por um usuário e considera esses locais "familiares". eventos de risco Olá é disparado quando entrar Olá ocorre de um local que não esteja na lista de saudação locais familiares. sistema de saudação tem um período inicial de assimilação de 30 dias, durante o qual ele não sinalizador quaisquer novos locais de locais desconhecidos. sistema Olá também ignora entradas de dispositivos conhecidos e locais geograficamente fechar local familiar tooa. 

### <a name="sign-ins-from-infected-devices"></a>Entradas de dispositivos infectados

Esse tipo de evento de risco identifica as entradas de dispositivos infectados com malware, que são conhecidos tooactively se comunicar com um servidor de bot. Isso é determinado correlacionando os endereços IP do dispositivo do usuário Olá endereços IP que estiveram em contato de um servidor de bot. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Entradas de endereços IP com atividade suspeita
Esse tipo de evento de risco identifica os endereços IP dos quais um grande número de tentativas de entrada com falha foram observadas, de várias contas de usuário e em um curto período de tempo. Isso faz a correspondência de padrões de tráfego de endereços IP usados por invasores e é um forte indicador contas ou já ou sobre toobe comprometida. Este é um algoritmo de aprendizado de máquina que ignora óbvio "*falsos positivos*", como endereços IP que são regularmente usadas por outros usuários na organização hello.  sistema Olá tem um período inicial de assimilação de 14 dias em que ele aprende comportamento entrada hello de um novo usuário e um novo locatário.


## <a name="detection-type"></a>Tipo de detecção

propriedade de tipo de detecção de saudação é um indicador (em tempo real ou Offline) para o período de detecção de saudação de um evento de risco.  
Atualmente, a maioria dos eventos de risco forem detectados como offline em uma operação de pós-processamento após a ocorrência de evento de risco de saudação.

Olá, a tabela a seguir lista a quantidade de saudação de tempo que leva para um tooshow de tipo de detecção para cima em um relatório relacionado:

| Tipo de Detecção | Relatório de latência |
| --- | --- |
| Tempo real | too10 5 minutos |
| Off-line | too4 2 horas |


Para tipos de eventos de risco Olá que detecta do Active Directory do Azure, os tipos de detecção de saudação são:

| Tipo de evento de risco | Tipo de detecção |
| :-- | --- | 
| [Usuários com credenciais vazadas](#leaked-credentials) | Off-line |
| [Entradas de endereços de IP anônimos](#sign-ins-from-anonymous-ip-addresses) | Tempo real |
| [Viagem impossível tooatypical locais](#impossible-travel-to-atypical-locations) | Off-line |
| [Entradas de locais desconhecidos](#sign-in-from-unfamiliar-locations) | Tempo real |
| [Entradas de dispositivos infectados](#sign-ins-from-infected-devices) | Off-line |
| [Entradas de endereços de IP com atividade suspeita](#sign-ins-from-ip-addresses-with-suspicious-activity) | Off-line|


## <a name="risk-level"></a>Nível de risco

propriedade de nível de risco de saudação de um evento de risco é um indicador (alto, médio ou baixo) para severidade hello e confiança Olá de um evento de risco. Essa propriedade ajuda ações Olá tooprioritize a que serem executadas. 

severidade de saudação do evento de risco Olá representa a força de saudação do sinal de saudação como um indicador de comprometimento de identidade.  
confiança Olá é um indicador para a possibilidade de saudação de falsos positivos. 

Por exemplo, 

* **Alta**: alta confiabilidade e evento de risco de alta severidade. Esses eventos são indicadores de alta seguras que Olá a identidade de usuário tiver sido comprometida, e as contas de usuário afetadas devem ser corrigidas imediatamente.

* **Média**: severidade alta, porém com evento de risco de baixa confiabilidade ou vice-versa. Esses eventos são potencialmente arriscados e quaisquer contas de usuário afetadas devem ser corrigidas.

* **Baixa**: baixa confiabilidade e evento de risco de baixa severidade. Esse evento não exigir uma ação imediata, mas quando combinado com outros eventos de risco, pode fornecer uma indicação de que Olá identidade for comprometida.

![Nível de risco](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>Credenciais vazadas

Vazamento credenciais eventos de risco são classificados como um **alta**, pois eles fornecem uma indicação clara que Olá nome de usuário e senha são invasor tooan disponíveis.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Entradas de endereços IP anônimos

nível de risco de Olá para esse tipo de evento de risco é **médio** porque um endereço IP anônimo não é uma forte indicação de um comprometimento de conta.  
É recomendável que você contate imediatamente Olá usuário tooverify se estivessem usando endereços IP anônimos.


### <a name="impossible-travel-tooatypical-locations"></a>Viagem impossível tooatypical locais

Viagem impossível geralmente é um bom indicador que um hacker foi toosuccessfully capaz de entrar. No entanto, falsos positivos podem ocorrer quando um usuário está viajando usando um novo dispositivo ou usando uma VPN que normalmente não é usada por outros usuários na organização hello. Outra fonte de falsos positivos é aplicativos que passam incorretamente servidor IPs como IPs, o que pode dar a aparência de saudação do cliente de logons que ocorrem do Centro de dados Olá onde o aplicativo do back-end está hospedado (geralmente, essas são data centers da Microsoft, que pode dar a aparência de saudação de logons ocorrendo da Microsoft propriedade endereços IP). Como resultado desses falsos positivos, nível de risco Olá para este evento de risco é **médio**.

> [!TIP]
> Você pode reduzir a quantidade de saudação de falso-positves relatados para esse tipo de evento de risco configurando [chamado locais](active-directory-named-locations.md). 

### <a name="sign-in-from-unfamiliar-locations"></a>Entrada de locais desconhecidos

Locais desconhecidos podem fornecer uma indicação de que um invasor for capaz de toouse uma identidade roubada. Falsos positivos podem ocorrer quando um usuário está viajando, experimentando um novo dispositivo ou usando uma nova VPN. Como resultado desses falsos positivos, nível de risco Olá para esse tipo de evento é **médio**.

### <a name="sign-ins-from-infected-devices"></a>Entradas de dispositivos infectados

Esse evento de risco identifica os endereços IP, não os dispositivos de usuário. Se vários dispositivos são atrás de um único endereço IP, e apenas alguns são controladas por uma rede de bot, entradas de outros dispositivos meu gatilho esse evento desnecessariamente, que é o motivo de saudação para classificar este evento de risco como **baixa**.  

É recomendável que você entre em contato com o usuário hello e verificar dispositivos do usuário Olá todos os. Também é possível que o dispositivo pessoal do usuário está infectado, ou como mencionado anteriormente, que outra pessoa estava usando um dispositivo infectado do hello mesmo endereço IP como usuário hello. Dispositivos infectados geralmente estão infectados por malware que ainda não foram identificados pelo software antivírus e também pode indicar como hábitos incorreto de usuário que podem ter causado Olá dispositivo toobecome infectado.

Para obter mais informações sobre como tooaddress infecções de malware, consulte Olá [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Entradas de endereços IP com atividade suspeita

É recomendável que você entre em contato com hello usuário tooverify se eles realmente entrou usando um endereço IP que foi marcado como suspeito. nível de risco de Olá para esse tipo de evento é "**médio**" porque vários dispositivos podem estar por trás de saudação mesmo endereço IP, enquanto somente alguns podem ser responsável pela atividade suspeita hello. 


 
## <a name="next-steps"></a>Próximas etapas

Eventos de risco são a base de saudação para proteger as identidades do AD do Azure. O Azure AD pode detectar seis eventos de risco atualmente: 


| Tipo de evento de risco | Nível de risco | Tipo de Detecção |
| :-- | --- | --- |
| [Usuários com credenciais vazadas](#leaked-credentials) | Alto | Off-line |
| [Entradas de endereços de IP anônimos](#sign-ins-from-anonymous-ip-addresses) | Média | Tempo real |
| [Viagem impossível tooatypical locais](#impossible-travel-to-atypical-locations) | Média | Off-line |
| [Entradas de locais desconhecidos](#sign-in-from-unfamiliar-locations) | Média | Tempo real |
| [Entradas de dispositivos infectados](#sign-ins-from-infected-devices) | Baixo | Off-line |
| [Entradas de endereços de IP com atividade suspeita](#sign-ins-from-ip-addresses-with-suspicious-activity) | Média | Off-line|

Onde você pode encontrar hello eventos de risco que foram detectados em seu ambiente?
Há dois locais em que você examinar os eventos de risco relatados:

 - **Relatórios do Azure AD** – eventos de risco são parte dos relatórios de segurança do Azure AD. Para obter mais detalhes, consulte Olá [usuários no relatório de riscos de segurança](active-directory-reporting-security-user-at-risk.md) e hello [relatório de segurança de logons arriscados](active-directory-reporting-security-risky-sign-ins.md).

 - **Azure AD Identity Protection** – eventos de risco também são parte das funcionalidades de relatório da [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
    

Enquanto o hello detecção de eventos de risco já representa um aspecto importante da proteção de suas identidades, você também tem Olá opção tooeither solucioná-los manualmente ou até mesmo implementar respostas automatizadas configurando políticas de acesso condicional. Para obter mais detalhes, confira [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
 
