---
title: "aaaSecurity alertas por tipo na Central de segurança do Azure | Microsoft Docs"
description: "Este artigo descreve os diferentes tipos de saudação de alertas de segurança disponíveis na Central de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Noções básicas de alertas de segurança na Central de Segurança do Azure
Este artigo ajuda toounderstand Olá diferentes tipos de alertas de segurança e informações relacionadas que estão disponíveis na Central de segurança do Azure. Para obter mais informações sobre como toomanage alertas e incidentes, consulte [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> tooset backup detecções avançadas, atualização tooAzure Central de segurança padrão. Há uma avaliação gratuita de 60 dias disponível. tooupgrade, selecione **preço** em Olá [política de segurança](security-center-policies.md). toolearn mais, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>Que tipo de alerta está disponível?
Central de segurança do Azure usa uma variedade de [recursos de detecção](security-center-detection-capabilities.md) tooalert clientes toopotential ataques direcionamento de seus ambientes. Esses alertas contêm informações valiosas sobre Olá o que disparou Olá alerta, recursos de saudação afetados e Olá a origem do ataque hello. informações de saudação incluídas em um alerta variam com base no tipo de saudação de análise usado toodetect Olá ameaça. Os Incidentes também podem conter informações contextuais adicionais que podem ser úteis ao investigar uma ameaça.  Este artigo fornece informações sobre Olá seguintes tipos de alerta:

* Análise de Comportamento da Máquina Virtual (VMBA)
* Análise de Rede
* Análise de Recursos
* Informações Contextuais

## <a name="virtual-machine-behavioral-analysis"></a>Análise de comportamento da máquina virtual
Central de segurança do Azure podem usar recursos de tooidentify comprometido de análise de comportamento com base na análise de logs de eventos de máquina virtual. Por exemplo, Eventos de Criação do Processos e Eventos de Logon. Além disso, há correlação com outros toocheck de sinais para dar suporte a evidência de uma campanha generalizada.

> [!NOTE]
> Para saber mais sobre como funcionam os recursos de detecção da Central de Segurança, confira [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md).
>

### <a name="crash-analysis"></a>Análise de falha
Análise de memória de despejo de falha é um método usado toodetect malware sofisticado que é capaz de tooevade as soluções tradicionais de segurança. Várias formas de malware tente tooreduce chance de saudação do está sendo detectada pelo produtos antivírus escrevendo nunca toodisk ou criptografando os componentes de software escritos toodisk. Isso torna Olá malware difícil toodetect por meio de abordagens tradicionais de antimalware. No entanto, esse tipo de malware pode ser detectado usando a análise de memória, porque o malware deve deixar rastreamentos na memória em ordem toofunction.

Quando o software falha, um despejo de captura uma parte da memória em tempo de saudação de travamento hello. Falha de saudação pode ser causada por malware, gerais do aplicativo ou problemas de sistema. Analisando a memória Olá no despejo hello, Central de segurança pode detectar técnicas usadas tooexploit vulnerabilidades no software, acessar dados confidenciais e clandestinamente persistir em um computador comprometido. Isso é feito com desempenho mínimo impacto toohosts como Olá análise é executada por Olá terminar de volta a Central de segurança.

Olá campos a seguir é toohello falha despejo alerta exemplos comuns que aparecem mais adiante neste artigo:

* O arquivo de despejo: O nome do arquivo hello despejo de memória.
* PROCESSNAME: O nome da saudação travamento do processo.
* PROCESSVERSION: Versão de hello travamento do processo.

### <a name="shellcode-discovered"></a>Shellcode descoberto
Código é carga Olá que é executada após o malware explora uma vulnerabilidade de software. Esse alerta indica que a análise do despejo de memória detectou um código executável com um comportamento normalmente executado por cargas mal-intencionadas. Embora software que não seja mal-intencionado possa executar esse comportamento, não é comum às práticas de desenvolvimento de software normal.

exemplo de alerta de código Hello fornece Olá campo adicional a seguir:

* ENDEREÇO: local de saudação na memória do código Olá shell.

Eis um exemplo desse tipo de alerta:

![Alerta de shellcode](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Descoberta de sequestro do módulo
O Windows usa bibliotecas de vínculo dinâmico (DLLs) tooallow software tooutilize comuns Windows funcionalidade do sistema. Captura de DLL ocorre quando malware alterado Olá DLL carga ordem tooload de ataques maliciosos na memória, em que um código arbitrário pode ser executado. Esse alerta indica que a análise de despejo de falha de saudação detectou um módulo nomeado da mesma forma que é carregado de dois caminhos diferentes. Um dos caminhos de saudação carregado vêm de um local de binários de sistema comuns do Windows.

Os desenvolvedores de software legítimo, ocasionalmente, alterar a ordem de carregamento DLL de saudação por motivos não mal-intencionado, como instrumentação, estendendo Olá SO Windows ou estender um aplicativo do Windows. toohelp diferenciar alterações mal-intencionados e potencialmente benignas toohello ordem de carregamento DLL, Central de segurança do Azure verifica se um módulo carregado está em conformidade perfil suspeitas tooa. resultado dessa verificação Olá é indicado pelo campo de "Assinatura" hello de alerta de saudação e é refletido na severidade Olá Olá alerta, descrição do alerta e etapas de correção de alerta. tooresearch se o módulo de saudação é legítima ou mal-intencionados, analisar Olá na cópia do hello captura o módulo de disco. Por exemplo, você pode verificar assinatura digital do arquivo hello, ou executar uma verificação antivírus.

Além disso toohello campos comuns descritos na seção anterior "código descobertos" do hello, esse alerta fornece Olá campos a seguir:

* ASSINATURA: Indica se Olá captura o módulo está em conformidade com tooa perfil de comportamento suspeito.
* HIJACKEDMODULE: nome de saudação do hello apoderar módulo de sistema do Windows.
* HIJACKEDMODULEPATH: o caminho de saudação do hello apoderar módulo de sistema do Windows.
* HIJACKINGMODULEPATH: caminho de saudação do módulo de roubo de saudação.

Eis um exemplo desse tipo de alerta:

![Alerta de sequestro de módulo](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Módulo do Windows simulado detectado
Malware pode usar nomes comuns dos binários do sistema do Windows (por exemplo, SVCHOST. EXE) ou módulos (por exemplo, NTDLL. DLL) muito*combinam* e oculte a natureza de saudação de um software mal-intencionado Olá dos administradores de sistema. Esse alerta indica que a análise de despejo de falha de saudação detecta que esse arquivo de despejo de falha Olá contém módulos que usam nomes de módulo de sistema do Windows, mas não atender a outros critérios que são típicos de módulos do Windows. Analisando Olá na cópia do disco do módulo mascarados Olá pode fornecem mais informações sobre natureza de legítimo ou mal-intencionado Olá deste módulo. A análise pode incluir:

* Confirme se que esse arquivo hello em questão é enviado como parte de um pacote de software legítimo.
* Verifique se a assinatura digital do arquivo hello.
* Execute uma verificação antivírus no arquivo hello.

Além disso toohello campos comuns descritos anteriormente na seção de "Código descoberto" Olá, esse alerta fornece Olá campos adicionais a seguir:

* DETALHES: Descreve se os metadados do módulo Olá são válido e se o módulo de saudação foi carregado de um caminho do sistema.
* NOME: o nome de saudação do módulo do Windows com hello.
* CAMINHO: Olá caminho toohello simulado módulo do Windows.

Esse alerta também extrai e exibe determinados campos de cabeçalho do módulo hello, como "CHECKSUM" e "TIMESTAMP". Esses campos são exibidos somente se houver campos Olá no módulo hello. Consulte Olá [Microsoft PE e COFF especificação](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) para obter detalhes sobre esses campos.

Eis um exemplo desse tipo de alerta:

![Alerta do Windows simulado](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Binário do sistema modificado descoberto
Malware pode modificar os principais binários do sistema em dados do access toocovertly ordem ou clandestinamente manter em um sistema comprometido. Esse alerta indica que análise de despejo de falha de saudação detectou principais binários do sistema operacional Windows foram modificados na memória ou no disco.

Os desenvolvedores de software legítimos ocasionalmente modificam módulos do sistema na memória por motivos lícitos, por exemplo, para desvios ou para compatibilidade de aplicativos. toohelp diferenciar entre módulos mal-intencionados e potencialmente legítimos, Central de segurança do Azure verifica se o módulo modificado Olá segue perfil suspeitas tooa. resultado dessa verificação Olá é indicado por severidade Olá Olá alerta, descrição do alerta e etapas de correção de alerta.

Além disso toohello campos comuns descritos anteriormente na seção de "Código descoberto" Olá, esse alerta fornece Olá campos adicionais a seguir:

* MODULENAME: O nome da saudação modificado binário de sistema.
* MODULEVERSION: A versão de hello modificado binário de sistema.

Eis um exemplo desse tipo de alerta:

![Alerta de binário do sistema](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Processo suspeito executado
Central de segurança identifica um processo suspeito que é executado na máquina de virtual de destino hello e, em seguida, dispara um alerta. detecção de saudação não procurará por nome específico hello, mas parecer para parâmetro de saudação do arquivo executável. Portanto, mesmo que o invasor Olá renomeia Olá executável, Central de segurança ainda pode detectar processo suspeitas hello.

Eis um exemplo desse tipo de alerta:

![Alerta de processo suspeito](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Várias contas de domínio consultadas
Central de segurança pode detectar várias tentativas tooquery contas de domínio do Active Directory, que é algo que normalmente executadas por invasores durante o reconhecimento de rede. Os invasores podem aproveitar essa técnica tooquery Olá tooidentify Olá os usuários do domínio, identificar contas de administrador de domínio hello, identificar computadores Olá que são controladores de domínio e também identificam Olá potencial domínio relação de confiança outros domínios.

Eis um exemplo desse tipo de alerta:

![Alerta de conta de vários domínios](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Os membros do grupo Administradores locais foram enumerados

Central de segurança será tootrigger um alerta quando o evento de segurança de saudação 4798, no Windows Server 2016 e Windows 10, é disparado. Isso acontece quando os grupos de administradores locais são enumerados, que é algo normalmente feito por invasores durante o reconhecimento de rede. Os invasores podem aproveitar essa identidade de saudação tooquery técnica de usuários com privilégios administrativos.

Eis um exemplo desse tipo de alerta:

![Administrador local](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Mistura anormal de caracteres maiúsculos e minúsculos

Central de segurança irá disparar um alerta quando ele detecta o uso de saudação de uma mistura de maiusculas e letras minúsculas na linha de comando de saudação. Alguns invasores podem usar este toohide técnica de maiusculas e minúsculas ou hash com base em regra de máquina.

Eis um exemplo desse tipo de alerta:

![Mistura anormal](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Ataque de tíquete do ouro do Kerberos

Um comprometido [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) chave pode ser usada por um invasor toocreate Kerberos "ouro" permissões, permitindo Olá invasor tooimpersonate qualquer usuário que desejarem. Central de segurança será tootrigger um alerta quando detectar esse tipo de atividade.

> [!NOTE] 
> Para saber mais sobre o Tíquete de ouro Kerberos, leia [Guia de atenuação de roubo de credenciais do Windows 10](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).

Eis um exemplo desse tipo de alerta:

![Tíquete de ouro](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Conta suspeita criada

A Central de Segurança vai disparar um alerta quando uma conta for criada com bastante semelhança à uma conta de privilégios de administrador interna existente. Essa técnica pode ser usada por invasores toocreate tooavoid ser percebido por humana verificação de conta de um invasor.
 
Eis um exemplo desse tipo de alerta:

![Conta suspeita](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Regra de firewall suspeita criada

Os invasores tente toocircumvent segurança de host por meio da criação de firewall personalizadas regras tooallow aplicativos mal-intencionados toocommunicate com o comando e controle ou toolaunch ataques por meio de rede Olá via Olá comprometido host. A Central de Segurança vai disparar um alerta quando detectar que uma nova regra de firewall foi criada de um arquivo executável em um local suspeito.
 
Eis um exemplo desse tipo de alerta:

![Regra de Firewall](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>Combinação suspeita de HTA e PowerShell

A Central de Segurança vai disparar um alerta quando detectar que um host de aplicativo HTML da Microsoft (HTA) está iniciando comandos do PowerShell. Essa é uma técnica usada pelos scripts de PowerShell invasores toolaunch mal-intencionado.
 
Eis um exemplo desse tipo de alerta:

![HTA e PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Análise de Rede
A detecção de ameaças da rede da Central de Segurança funciona coletando automaticamente as informações de segurança de seu tráfego do Azure IPFIX (Internet Protocol Flow Information Export). Ele analisa essas informações, geralmente correlacionando informações de várias fontes, tooidentify ameaças.

### <a name="suspicious-outgoing-traffic-detected"></a>Tráfego de saída suspeito detectado
Dispositivos de rede podem ser descobertos e descritos muito Olá mesma maneira que outros tipos de sistemas. Os invasores normalmente começam com verificação de porta ou varredura de porta. No exemplo a seguir Olá, você deve ter tráfego suspeito do Secure Shell (SSH) de uma VM. Nesse cenário, é possível usar força bruta de SSH ou um ataque de varredura de porta contra um recurso externo.

![Alerta de tráfego de saída suspeito](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Esse alerta fornece informações que você pode usar recursos de saudação tooidentify que foi usado tooinitiate esse ataque. Esse alerta também fornece informações tooidentify Olá comprometido máquina, tempo de detecção de saudação, além de protocolo de saudação e porta que foi usada. Esta folha também fornece uma lista de etapas de correção que pode ser usado toomitigate esse problema.

### <a name="network-communication-with-a-malicious-machine"></a>Comunicação de rede com uma máquina mal-intencionada
Aproveitando os feeds de inteligência de ameaças da Microsoft, a Central de Segurança do Azure pode detectar máquinas comprometidas que estão se comunicando com endereços IP mal-intencionados. Em muitos casos, o endereço mal-intencionado Olá é um centro de comando e controle. Nesse caso, a Central de segurança detectou que comunicação Olá foi feita usando o malware presente carregador (também conhecido como [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![alerta de comunicação de rede](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Esse alerta fornece informações que permitem recursos de saudação tooidentify que foi usado tooinitiate esse ataque, Olá atacados recursos, Olá vítima IP, Olá invasor IP e tempo de detecção de saudação.

> [!NOTE]
> Endereços IP ativos foram removidos nesta captura de tela por fins de privacidade.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Possível saída do ataque de negação de serviço detectada
Anormal tráfego de rede que se origina de uma máquina virtual pode causar tootrigger Central de segurança, um tipo de negação de serviço potencial de ataque.

Eis um exemplo desse tipo de alerta:

![DOS de Saída](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Análise de Recursos
Análise de recursos da Central de segurança se concentra na plataforma como um serviços de serviço (PaaS), como a integração de saudação com hello [detecção de ameaças do banco de dados do Azure SQL](../sql-database/sql-database-threat-detection.md) recurso. Central de segurança com base nos resultados da análise de saudação dessas áreas, dispara um alerta de recurso.

### <a name="potential-sql-injection"></a>Potencial injeção de SQL
Injeção de SQL é um ataque em que o código mal-intencionado é inserido em cadeias de caracteres que são passadas posteriormente tooan instância do SQL Server para análise e execução. Qualquer procedimento que constrói instruções SQL deve ser revisado em busca de vulnerabilidades de injeção, pois o SQL Server executa todas as consultas sintaticamente válidas que recebe. Detecção de ameaças SQL usa anomalias detecção toodetermine eventos suspeitos que podem estar ocorrendo em seus bancos de dados do SQL Azure, a análise comportamental e aprendizado de máquina. Por exemplo:

* Tentativa de acesso do banco de dados por um antigo funcionário
* Ataques de injeção de SQL
* Banco de dados do access incomum tooa produção de um usuário em casa

![Alerta de Potencial Injeção de SQL](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

informações de Olá neste alerta podem ser usados tooidentify Olá atacado recursos, tempo de detecção de saudação e estado de Olá de ataque de saudação. Ele também fornece um link toofurther etapas de investigação.

### <a name="vulnerability-toosql-injection"></a>Vulnerabilidade tooSQL injeção
Este alerta é disparado quando um erro de aplicativo é detectado em um banco de dados. Esse alerta pode indicar a que ataques de injeção de tooSQL uma possível vulnerabilidade.

![Alerta de Potencial Injeção de SQL](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Acesso incomum de um local desconhecido
Este alerta é disparado quando um evento de acesso de um endereço IP desconhecido foi detectado no servidor de saudação, que não foi vista na Olá último período.

![Alerta de acesso incomum](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Informações Contextuais
Durante uma investigação, analistas necessário contexto extra tooreach um veredicto sobre a natureza de saudação de ameaça à saudação e como toomitigate-lo.  Por exemplo, uma anomalia de rede foi detectada, mas sem Noções básicas sobre o que mais está acontecendo na rede de saudação ou com o recurso de toohello destinada de relação ele estará cada disco rígido toounderstand tootake quais ações. tooaid com isso, um incidente de segurança podem incluir artefatos, eventos relacionados e informações que podem ajudar investigador hello. Olá disponibilidade de informações adicionais irão variar com base na Olá tipo de ameaça detectada Olá a configuração de seu ambiente e não estará disponível para todos os incidentes de segurança.

Se informações adicionais estão disponíveis, ele será mostrado em Olá incidente de segurança abaixo lista Olá de alertas. Isso pode conter informações como:

- Limpar eventos do log
- Dispositivo PNP conectado de dispositivo desconhecido
- Alertas que não são acionáveis 

![Alerta de acesso incomum](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Consulte também
Neste artigo, você aprendeu sobre os diferentes tipos de saudação de alertas de segurança na Central de segurança. toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Manipulação de incidente de segurança na Central de Segurança do Azure](security-center-incident.md)
* [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md)
* [Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md)
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md): perguntas frequentes sobre como usar o serviço de saudação de localizar.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) encontre postagens no blog sobre conformidade e segurança do Azure.
