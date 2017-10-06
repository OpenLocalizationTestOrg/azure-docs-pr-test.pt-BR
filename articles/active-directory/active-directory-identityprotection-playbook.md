---
title: "Guia estratégico de proteção de identidade do Active Directory aaaAzure | Microsoft Docs"
description: "Saiba como Azure AD Identity Protection permite que você toolimit capacidade Olá tooexploit um invasor uma identidade comprometida ou dispositivo e toosecure uma identidade ou um dispositivo que era anteriormente conhecido ou suspeita toobe comprometido."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Guia estratégico do Azure Active Directory Identity Protection
Este guia estratégico vai ajudá-lo a:

* Preencher os dados no ambiente de proteção de identidade hello, simulando eventos de risco e vulnerabilidades
* Configurar políticas de acesso condicional com base em risco e teste o impacto Olá dessas políticas

## <a name="simulating-risk-events"></a>Simulação de Eventos de Risco
Esta seção fornece as etapas para simular Olá seguintes tipos de eventos de risco:

* Entradas de endereços IP anônimos (fácil)
* Entradas de locais desconhecidos (moderado)
* Viagem impossível tooatypical locais (difícil)

Outros eventos de risco não podem ser simulados de maneira segura.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Entradas de endereços IP anônimos
Esse tipo de evento de risco identifica os usuários que entraram com êxito de um endereço IP que foi identificado como um endereço IP de proxy anônimo. Esses proxies são usados por pessoas que desejam toohide endereço IP do seu dispositivo e podem ser usadas com objetivos mal-intencionados.

**toosimulate uma entrada de um IP anônimo, executar Olá etapas**:

1. Baixar Olá [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).
2. Usando o hello Tor Browser, navegue muito[https://myapps.microsoft.com](https://myapps.microsoft.com).   
3. Insira as credenciais de saudação da conta de saudação desejado tooappear em hello **entradas de endereços IP anônimos** relatório.

Olá entrar aparecerão no painel de proteção de identidade Olá em 5 minutos. 

### <a name="sign-ins-from-unfamiliar-locations"></a>Entradas de locais desconhecidos
risco de locais desconhecidos Hello é um mecanismo de avaliação de entrada em tempo real que considera após entrar locais (IP, Latitude / Longitude e ASN) toodetermine locais de novo / desconhecidos. sistema de saudação armazena IPs anterior, Latitude / Longitude e ASNs de um usuário e considera esses locais familiares toobe. Um local de entrada é considerado familiarizado se hello local de entrada não corresponde a nenhum dos locais familiares existente de saudação.

Azure Active Directory Identity Protection:  

* tem um período inicial de aprendizado de 14 dias, durante o qual ele não sinaliza nenhum local novo como desconhecido.
* ignora entradas de dispositivos conhecidos e locais geograficamente fechar tooan local existente de familiar.

toosimulate de locais desconhecidos, você tem toosign em um local e o dispositivo conta Olá não entrou de antes. 

**toosimulate uma entrada de um local desconhecido, executar Olá etapas**:

1. Escolha uma conta com um histórico de entrada de, pelo menos, 14 dias. 
2. Realize uma das seguintes opções:
   
   a. Durante o uso de uma VPN, navegue muito[https://myapps.microsoft.com](https://myapps.microsoft.com) e digite as credenciais de saudação da conta de Olá você deseja que o evento de risco toosimulate hello para.
   
   b. Peça um colega no toosign local diferente usando credenciais da conta da saudação (não recomendadas).

Olá entrar aparecerão no painel de proteção de identidade Olá em 5 minutos.

### <a name="impossible-travel-tooatypical-location"></a>Viagem impossível tooatypical local
Simulando a condição de viagem impossível Olá é difícil porque o algoritmo de saudação usa tooweed de aprendizado de máquina out falsos positivos, como viagem impossível de dispositivos conhecidos ou entradas de VPNs são usadas por outros usuários no diretório de saudação. Além disso, o algoritmo de saudação exige um histórico de entrada de 3 dias too14 para usuário Olá antes de começar a gerar eventos de risco.

**toosimulate um local tooatypical viagem impossível executar Olá etapas**:

1. Usando o navegador padrão, navegue muito[https://myapps.microsoft.com](https://myapps.microsoft.com).  
2. Insira as credenciais de saudação da conta de saudação para que você deseja toogenerate um evento de risco de viagem impossível.
3. Altere o agente do usuário. É possível alterar o agente do usuário no Internet Explorer nas Ferramentas de Desenvolvedor ou então no Firefox ou Chrome usando um complemento de alternador de agente do usuário.
4. Altere seu endereço IP. É possível alterar seu endereço IP usando uma VPN, um complemento do Tor ou criando um novo computador no Azure em um diferente.
5. Entrada muito[https://myapps.microsoft.com](https://myapps.microsoft.com) usando Olá as mesmas credenciais como antes e após alguns minutos depois de entrar anterior Olá.

Olá entrar aparecerá no painel de proteção de identidade hello dentro de 2 a 4 horas.<br>
Devido a saudação complexos de aprendizado de máquina modelos envolvidos, há uma possibilidade que ele será não escolhido.<br> Você pode querer tooreplicate essas etapas de várias contas do AD do Azure.

## <a name="simulating-vulnerabilities"></a>Simulação de vulnerabilidades
Vulnerabilidades são pontos fracos no seu ambiente do Azure AD que podem ser explorados por um ator maligno. Atualmente, três tipos de vulnerabilidades são exibidas no Azure AD Identity Protection que aproveitam os outros recursos do Azure AD. Essas vulnerabilidades serão exibidas no painel de proteção de identidade Olá automaticamente depois que esses recursos são configurados.

* Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="user-compromise-risk"></a>Risco de comprometimento do usuário
**tootest risco de comprometimento do usuário, executar Olá etapas**:

1. Entrada muito[https://portal.azure.com](https://portal.azure.com) com credenciais de administrador global para seu locatário.
2. Navegue muito**Identity Protection**. 
3. Em Olá principal **Azure AD Identity Protection** folha, clique em **configurações**. 
4. Em Olá **configurações do Portal** folha, em **as regras de segurança**, clique em **o risco de comprometimento do usuário**. 
5. Em Olá **entrar risco** folha, ativar **Habilitar regra** off e, em seguida, clique em **salvar** configurações.
6. Para uma determinada conta de usuário, simule um evento de risco de locais desconhecidos ou IP anônimo. Isso será elevar o nível de risco do usuário Olá para esse usuário muito**médio**.
7. Aguarde alguns minutos e verifique se o nível do usuário é **Médio**.
8. Vá toohello **configurações do Portal** folha.
9. Em Olá **o risco de comprometimento do usuário** folha, em **Habilitar regra**, selecione **em** . 
10. Selecione uma saudação as opções a seguir:
    
    a. tooblock, selecione **médio** em **bloco entrar**.
    
    b. alteração de senha segura tooenforce, selecione **médio** em **exigir autenticação multifator**.
11. Clique em **Salvar**.
12. Agora você pode testar o acesso condicional baseado em risco ao entrar usando um usuário com um nível de risco elevado. Se o risco de usuário Olá é médio, dependendo da configuração de saudação de sua política, sua entrada no é a ser bloqueada ou são forçados toochange sua senha. 
    <br><br>
    ![Guia estratégico](./media/active-directory-identityprotection-playbook/201.png "manual")
    <br>

## <a name="sign-in-risk"></a>Risco de entrada
**tootest um sinal de risco, execute Olá etapas a seguir:**

1. Entrada muito[https://portal.azure.com ](https://portal.azure.com) com credenciais de administrador global para seu locatário.
2. Navegue muito**Identity Protection**.
3. Em Olá principal **Azure AD Identity Protection** folha, clique em **configurações**. 
4. Em Olá **configurações do Portal** folha, em **as regras de segurança**, clique em **entrar risco**.
5. Em hello * * entrar risco * * folha, selecione **na** em **Habilitar regra**. 
6. Selecione uma saudação as opções a seguir:
   
   a. tooblock, selecione **médio** em **bloco entrar**
   
   b. alteração de senha segura tooenforce, selecione **médio** em **exigir autenticação multifator**.
7. tooblock, selecione média em bloco entrar.
8. autenticação de multifator tooenforce, selecione **médio** em **exigir autenticação multifator**.
9. Clique em **Save**.
10. Agora você pode testar o acesso condicional com base em risco, simulando locais desconhecidos hello ou IP anônimo corre o risco de eventos porque os dois são **médio** eventos de risco.


![Guia estratégico](./media/active-directory-identityprotection-playbook/200.png "Guia estratégico")


## <a name="see-also"></a>Consulte também
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

