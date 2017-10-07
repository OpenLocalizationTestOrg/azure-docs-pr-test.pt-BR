---
title: "aaaAzure Active Directory conectar integridade perguntas Frequentes – Azure | Microsoft Docs"
description: "Encontre respostas para perguntas frequentes sobre o Azure AD Connect Health. Estas perguntas frequentes abordam dúvidas sobre como usar o serviço de hello, incluindo Olá modelo, recursos, limitações e suporte de cobrança."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Perguntas frequentes do Azure AD Connect Health
Este artigo inclui respostas toofrequently perguntas frequentes (FAQs) sobre integridade de conexão do Azure Active Directory (AD do Azure). As perguntas frequentes abrangem perguntas sobre como toouse Olá serviço, que inclui a saudação modelo, recursos, limitações e suporte de cobrança.

## <a name="general-questions"></a>Perguntas gerais
**P: Eu gerencio vários diretórios do Azure AD. Como alternar toohello que possui o Azure Active Directory Premium?**

tooswitch entre diferentes do Azure AD locatários, selecione Olá conectado no momento **nome de usuário** em Olá canto superior direito e escolha conta apropriada hello. Se a conta de saudação não estiver listada aqui, selecione **sair**, e, então, usar credenciais de administrador global saudação do diretório Olá com o Azure Active Directory Premium toosign no.

**P: Qual versão de funções de identidade tem suporte do Azure AD Connect Health?**

Olá tabela a seguir lista as funções hello e versões de sistema operacional com suporte.

|Função| Sistema Operacional/Versão|
|--|--|
|Suporte para os Serviços de Federação do Active Directory (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | Versão 1.0.9125 ou superior|
|Active Directory Domain Services (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Observe que recursos Olá fornecidos pelo serviço Olá podem ser diferente com base na função de saudação e de sistema operacional de saudação. Em outras palavras, todos os recursos de saudação podem não estar disponíveis para todas as versões de sistema operacional. Consulte as descrições de recurso Olá para obter detalhes.

**P: quantas licenças são necessário toomonitor minha infra-estrutura?**

* Olá, agente de integridade de se conectar primeiro requer pelo menos uma licença Azure AD Premium.
* Cada agente registrado adicional requer 25 licenças Azure AD Premium adicionais.
* Contagem de agente é equivalente toohello o número total de agentes que estão registrados em todas as funções monitoradas (AD FS, o Azure AD Connect e AD DS).

Informações de licenciamento também foi encontradas no hello [página de preços do Azure AD](https://aka.ms/aadpricing).

Exemplo:

| Agentes registrados | Licenças necessárias | Configuração de monitoramento de exemplo |
| ------ | --------------- | --- |
| 1 | 1 | Um servidor de conexão do Azure AD |
| 2 | 26| Um servidor do Azure AD Connect e um controlador de domínio |
| 3 | 51 | Um servidor dos Serviços de Federação do Active Directory (AD FS), um proxy do AD FS e um controlador de domínio |
| 4 | 76 | Um servidor do AD FS, um proxy do AD FS e dois controladores de domínio |
| 5 | 101 | Um servidor do Azure AD Connect, um servidor do AD FS, um proxy AD FS e dois controladores de domínio |


## <a name="installation-questions"></a>Perguntas sobre a instalação

**P: qual é o impacto de saudação da instalação do agente do Azure AD Connect Health da saudação em servidores individuais?**

impacto de saudação de instalar servidores de proxy de aplicativo web do hello Microsoft Azure agente AD Connect Health, o AD FS, servidores do Azure AD Connect (sincronização), controladores de domínio é mínimo com respeito toohello CPU, consumo de memória, largura de banda de rede e armazenamento.

Olá números a seguir é uma aproximação:

* Consumo de CPU: aumento de aproximadamente 1 a 5%.
* Consumo de memória: % too10 Olá total da memória do sistema.

> [!NOTE]
> Se o agente de saudação não pode se comunicar com o Azure, agente Olá armazena dados de saudação localmente para um limite máximo definido. Agente de saudação substitui hello "cache" dados "reparada menos recentemente".
>
>

* Armazenamento em buffer local para Agentes do Azure AD Connect Health: aproximadamente 20 MB.
* Para servidores do AD FS, é recomendável que você forneça um espaço em disco de 1.024 MB (1 GB) para o canal de auditoria de saudação do AD FS para agentes de integridade de conexão de AD do Azure tooprocess todos os dados de auditoria de saudação antes que ele será substituído.

**P: posso terá tooreboot meus servidores durante a instalação de saudação de agentes de integridade de conectar Olá AD do Azure?**

Não. instalação de saudação de agentes de saudação não exigirá servidor Olá tooreboot. No entanto, a instalação de algumas etapas de pré-requisito pode exigir uma reinicialização do servidor de saudação.

Por exemplo, no Windows Server 2008 R2, a instalação do .NET Framework 4.5 requer a reinicialização do servidor.

**P: Os Serviços do Azure AD Connect Health funcionam por meio de um proxy HTTP de passagem?**

Sim. Para operações contínuas, você pode configurar um solicitações HTTP proxy tooforward saída HTTP toouse do agente de integridade de saudação.
Leia mais sobre [configurar HTTP Proxy para agentes de integridade](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Se você precisar tooconfigure um proxy durante o registro do agente, talvez seja necessário toomodify suas configurações de Proxy do Internet Explorer com antecedência.

1. Abra Internet Explorer -> **Configurações** > **Opções de Internet** > **Conexões** > **Configurações da LAN**.
2. Selecione **Usar um Servidor Proxy para a LAN**.
3. Selecione **Avançado** se você tiver portas de proxy diferentes para HTTP e HTTPS/Seguro.

**P: não autenticação básica do Azure AD Connect Health suporte quando se conectar tooHTTP proxies?**

Não. Um mecanismo toospecify um nome de usuário arbitrários e uma senha para a autenticação básica não é suportada atualmente.

**P: o que fazem as portas de firewall preciso tooopen para toowork do agente de integridade de conexão de saudação do AD do Azure?**

Consulte Olá [seção requisitos](active-directory-aadconnect-health-agent-install.md#requirements) para lista de saudação de portas de firewall e outros requisitos de conectividade.

**P: por que vejo que os dois servidores com hello mesmo nome no portal de integridade de conexão de saudação do AD do Azure?**

Quando você remove um agente de um servidor, servidor de saudação não é removido automaticamente do portal do Azure AD Connect Health hello. Se você remove um agente de um servidor ou remove o próprio servidor de saudação manualmente, será necessário entrada do servidor de saudação do toomanually delete do portal de integridade de conexão de saudação do AD do Azure.

Você pode refazer a imagem de um servidor ou criar um novo servidor com hello mesmo detalhes (como o nome do computador). Se você não removeu o servidor já registrado saudação do portal de integridade de conexão de saudação do AD do Azure, e você instalou o agente de saudação no novo servidor de saudação, você poderá ver duas entradas com hello mesmo nome.

Nesse caso, exclua manualmente a entrada hello que pertence o servidor mais antigo toohello. dados Olá para esse servidor devem estar desatualizados.

## <a name="health-agent-registration-and-data-freshness"></a>Registro de Agente de Integridade e atualização de dados

**P: quais são os motivos comuns para falhas de registro do agente de integridade de saudação e como solucionar problemas?**

Olá agente de integridade pode falhar tooregister devido a seguir toohello motivos possíveis:

* Agente de saudação não pode se comunicar com pontos de extremidade Olá necessário porque um firewall está bloqueando o tráfego. Isso é especialmente comum em servidores proxy de aplicativo Web. Certifique-se de que você permitiu portas e os pontos de extremidade de toohello necessária a comunicação de saída. Consulte Olá [seção requisitos](active-directory-aadconnect-health-agent-install.md#requirements) para obter detalhes.
* Comunicação de saída está sujeito tooan inspeção de SSL pela camada de rede hello. Isso faz com que o certificado de saudação que o agente Olá usa toobe substituída pela entidade da servidor Olá inspeção e falha de registro de agente Olá etapas toocomplete hello.
* Olá usuário não tem acesso tooperform Olá registro do agente de saudação. Por padrão, os administradores globais têm acesso. Você pode usar [controle de acesso baseado em função](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate acesso tooother usuários.

**P: eu estou obtendo alertado que "dados de serviço de integridade não são a toodate." Como solucionar problemas de problema Olá?**

O Azure AD Connect Health gera um alerta de saudação quando não receber todos os pontos de dados de saudação do servidor de saudação em Olá últimas duas horas. Pode haver várias razões para esse alerta ser acionado.

* Agente de saudação não pode se comunicar com pontos de extremidade Olá necessário porque um firewall está bloqueando o tráfego. Isso é especialmente comum em servidores proxy de aplicativo Web. Certifique-se de que você tem permissão de pontos de extremidade de toohello necessária a comunicação de saída e as portas. Consulte Olá [seção requisitos](active-directory-aadconnect-health-agent-install.md#requirements) para obter detalhes.
* Comunicação de saída está sujeito tooan inspeção de SSL pela camada de rede hello. Isso faz com que o certificado de saudação que agente Olá usa toobe substituída pela entidade da servidor Olá inspeção e processo Olá falha serviço de Azure AD Connect Health tooupload dados toohello.
* Você pode usar o comando de conectividade de saudação incorporado ao agente hello. [Leia mais](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* agentes de saudação também dão suporte a conectividade de saída por meio de um HTTP Proxy não autenticado. [Leia mais](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Perguntas sobre operações
**P: é necessário tooenable auditoria em servidores de proxy de aplicativo web Olá?**

Não, a auditoria não precisa toobe habilitado em servidores de proxy de aplicativo web hello.

**P: Como Alertas do Azure AD Connect Health são resolvidos?**

Alertas do Azure AD Connect Health são resolvidos em uma condição de êxito. Agentes de integridade de conexão de AD do Azure detectar e relatar o serviço de toohello de condições de sucesso Olá periodicamente. Para alguns alertas, a supressão de saudação é baseada em tempo. Em outras palavras, se hello mesma condição de erro não for observada dentro de 72 horas da geração de alertas, Olá alerta será resolvido automaticamente.

**P: eu estou obtendo alertado que "a solicitação de autenticação de teste (transações sintéticas) falha tooobtain um token". Como solucionar problemas de problema Olá?**

O Azure AD Connect Health para AD FS gera este alerta quando Olá instalado em um servidor do AD FS do agente de integridade não tooobtain um token como parte de uma transação sintética iniciada pelo Olá agente de integridade. Agente de integridade de saudação tentativas tooget um token para uma terceira parte confiável self e usa o contexto do sistema local hello. Este é um tooensure de captura todos os testes do AD FS está em um estado de emissão de tokens.

Geralmente este teste falha porque Olá agente de integridade é nome do farm de saudação do AD FS tooresolve não é possível. Isso pode acontecer se servidores do hello AD FS estão atrás de um balanceador de carga de rede e solicitação de saudação obtém iniciada de um nó que está por trás do balanceador de carga de saudação (como tooa contrário cliente regular que está na frente do balanceador de carga de saudação). Isso pode ser corrigido pela atualização do arquivo de hosts"hello" localizado em "C:\WINDOWS\system32\drivers\etc." tooinclude Olá endereço do servidor de saudação do AD FS ou um endereço IP de loopback (127.0.0.1) para o nome do farm de saudação do AD FS (por exemplo, sts.contoso.com). Adicionando arquivo de host Olá curto-circuito chamada de rede hello, permitindo assim que o token de Olá Olá agente de integridade tooget.

**P: recebi um email indicando que minhas máquinas não são corrigidas para ataques de ransomeware recentes hello. Por que eu recebi esse email?**

Serviço de integridade de conexão do AD do Azure examinados Olá todas as máquinas que ele monitora os patches do tooensure Olá necessários foram instaladas. email de Olá foi enviado a administradores de inquilinos toohello se pelo menos um computador não tivesse patches críticos hello. Olá lógica a seguir foi usado toomake essa determinação.
1. Localize todos os hotfixes Olá instalados na máquina de saudação.
2. Verifique se pelo menos um dos Olá HotFixes do hello definido lista está presente.
3. Em caso afirmativo, a máquina de saudação está protegida. Caso contrário, a máquina hello está em risco de ataque de saudação.

Você pode usar Olá tooperform de script do PowerShell a seguir essa verificação manualmente. Ele implementa Olá acima lógica.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>Links relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalação do Agente do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operações de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Usando o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [Histórico de versão do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
