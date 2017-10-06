---
title: "aaaConnector histórico de lançamento de versão | Microsoft Docs"
description: "Este tópico lista todas as versões do hello conectores para o Forefront Identity Manager (FIM) e o Microsoft Identity Manager (MIM)"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>Histórico de lançamento de versão do conector
Olá conectores para o Forefront Identity Manager (FIM) e o Microsoft Identity Manager (MIM) são atualizados com frequência.

> [!NOTE]
> Este tópico é somente para FIM e MIM. Esses conectores não são suportados para instalação no Azure AD Connect. Conectores lançados pré-instaladas em AADConnect ao atualizar toospecified compilação.

Este tópico lista todas as versões do hello conectores que foram lançadas.

Links relacionados:

* [Baixar os Conectores mais recentes](http://go.microsoft.com/fwlink/?LinkId=717495)
* [Conector LDAP Genérico](active-directory-aadconnectsync-connector-genericldap.md)
* [Conector do SQL Genérico](active-directory-aadconnectsync-connector-genericsql.md)
* [Conector dos Serviços Web](http://go.microsoft.com/fwlink/?LinkID=226245)
* [Conector do PowerShell](active-directory-aadconnectsync-connector-powershell.md)
* [Conector do Lotus Domino](active-directory-aadconnectsync-connector-domino.md)


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (AADConnect versão pendente)


### <a name="fixed-issues"></a>Problemas corrigidos:

* Serviços Web genéricos:
  * Correção de um problema que estava impedindo um projeto SOAP de ser criado quando havia dois ou mais pontos de extremidade.
* SQL genérico:
  * Na operação de saudação da importação Olá GSQL foi não converter tempo corretamente, quando salvo tooconnector espaço. Olá formato de data e hora padrão para o espaço do conector de saudação GSQL foi alterado de 'AAAA-MM-dd: ssZ' too'yyyy-MM-dd: ssZ '.

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Problemas corrigidos:

* Serviços Web genéricos:
  * ferramenta de como Wsconfig Olá não converteu corretamente matriz Json de saudação de "solicitação de exemplo" para o método de serviço REST hello. Isso causava problemas com a serialização essa matriz Json para solicitação REST hello.
  * A Ferramenta de Configuração do Conector do Serviço Web não dá suporte ao uso de símbolos de espaço em nomes de atributo JSON 
    * Um padrão de substituição pode ser adicionado manualmente toohello WSConfigTool.exe.config arquivo, por exemplo```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes:
  * Olá quando a opção **permitir certifiers personalizadas para as unidades organizacionais/organização** está desabilitado Olá conector falhar durante a exportação (atualização) depois que todos os atributos de fluxo de exportação hello serão exportado tooDomino, mas no tempo de saudação do Exportar um KeyNotFoundException é retornado tooSync. 
    * Isso acontece porque Olá renomear operação falhar quando ele tenta toochange DN (atributo de nome de usuário) alterando um dos atributos de saudação abaixo:  
      - Sobrenome
      - Nome
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - ou
      - altcommonname

  * Quando a opção **Permitir certificadores personalizados para a organização/as unidades organizacionais** está habilitada, mas os certificadores necessários ainda estão vazios, ocorre uma KeyNotFoundException.

### <a name="enhancements"></a>Melhorias:

* SQL genérico:
  * **Cenário: reprojetado implementado:** recurso "*"
  * **Descrição da solução:** abordagem alterada para a [manipulação de atributos de referência de vários valores](active-directory-aadconnectsync-connector-genericsql.md).


### <a name="fixed-issues"></a>Problemas corrigidos:

* Serviços Web genéricos:
  * Não será possível importar a configuração do servidor se houver um Conector WebService
  * O Conector WebService não está funcionando com vários Serviços Web

* SQL genérico:
  * Nenhum tipo de objeto é listado para o atributo de referência de valor único
  * A importação delta na estratégia de Controle de Alterações exclui o objeto quando o valor é removido da tabela de vários valores
  * OverflowException no conector GSQL com DB2 no AS/400

Lotus:
  * Opção adicional tooenable\disable pesquisando UOs antes de abrir a página GlobalParameters

## <a name="114430"></a>1.1.443.0

Lançamento: março de 2017

### <a name="enhancements"></a>Melhorias

* SQL genérico:</br>
  **Cenário sintomas:** é uma limitação conhecida com hello conector do SQL onde podemos permitir somente um tipo de objeto de tooone de referência e exigem uma referência cruzada com membros. </br>
  **Descrição da solução:** na etapa de processamento de saudação para referências foram "*" opção for escolhida, todas as combinações de tipos de objeto serão retornadas o mecanismo de sincronização toohello voltar.

>[!Important]
- Isso cria vários espaços reservados
- É necessário toomake se Olá de nomenclatura é exclusivo entre tipos de objeto.


* LDAP genérico:</br>
 **Cenário:** quando apenas alguns contêineres são selecionados na partição específica, em seguida, pesquisa Olá ainda será feita na partição inteira. O específico será filtrado pelo serviço de sincronização, mas não pelo MA que pode causar degradação do desempenho. </br>

 **Descrição da solução:** toomake de código do conector alterado GLDAP possível passar por todos os contêineres e pesquisar objetos em cada um deles, em vez de procurar na partição inteira hello.


* Lotus Domino:

  **Cenário:** o suporte para exclusão de email Domino para a remoção de pessoa durante uma exportação. </br>
  **Solução:** suporte para exclusão de email configurável para a remoção de pessoa durante uma exportação.

### <a name="fixed-issues"></a>Problemas corrigidos:
* Serviços Web genéricos:
 * Ao alterar a URL do serviço de saudação padrão como SAP wsconfig projetos por meio da ferramenta de configuração do serviço Web, em seguida, Olá erro a seguir ocorre: não foi possível localizar uma parte do caminho de saudação

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* LDAP genérico:
 * O conector de GLDAP não verá todos os atributos no AD LDS
 * Assistente quebras quando nenhum atributo UPN é detectado do esquema de diretório LDAP Olá
 * Quando o atributo de "objectclass" não está selecionado, há falha na importação Delta com erros de descoberta não presentes durante a importação completa
 * Uma página de configuração "Configurar partições e hierarquias", não mostra todos os objetos que tipo é partição toohello igual para servidores Novel Olá genérico  
LDAP MA. Eles exibem apenas objetos de partição RootDSE.


* SQL genérico:
 * Fixo para bug de atributo com multivalores de importação Delta de marca d'água de SQL não importado
 * Ao exportar valores excluídos/adicionados de atributo com multivalores, eles não são excluídos/adicionados na fonte de dados.  


* Lotus Notes:
 * Um campo específico "Nome completo" é mostrado no metaverso Olá corretamente no entanto quando exportar tooNotes Olá valor para o atributo de saudação é nulo ou vazio.
 * Fixo para o erro de certificador de duplicata
 * Quando Olá objeto sem nenhum dado for selecionado no hello Lotus Domino conector com outros objetos que recebemos erro de descoberta de saudação ao executar importação completa.
 * Quando a importação de Delta é sendo executar em Olá Lotus Domino conector, final Olá Olá que execute, Microsoft.IdentityManagement.MA.LotusDomino.Service.exe serviço às vezes, retorna um erro de aplicativo.
 * Associação de grupo geral funciona bem e é mantida, exceto durante a execução Olá exportação tootry tooremove um usuário da associação mostra como êxito com uma atualização, mas o usuário hello, na verdade, não é removido da associação em Lotus Notes.
 * Um modo de toochoose oportunidade de exportação como "Acrescentar o Item na parte inferior" foi adicionado na configuração de GUI do Lotus MA tooappend novos itens na parte inferior durante a exportação de saudação para atributos com valores múltiplos.
 * Conector adicionará Olá necessário arquivo de saudação toodelete lógica da pasta de emails de saudação e ID do cofre.
 * Exclua a associação que não estiver funcionando para membro NAB cruzado.
 * Os valores devem ser excluídos com êxito do atributo de multivalores

## <a name="111170"></a>1.1.117.0
Lançamento: março de 2016

**Novo Conector**  
Versão da saudação inicial [conector do SQL genérico](active-directory-aadconnectsync-connector-genericsql.md).

**Novos recursos:**

* Conector LDAP Genérico:
  * Adicionado suporte para importação delta com o Isode.
* Conector dos Serviços Web:
  * Olá atualizada csEntryChangeResult atividade e setImportErrorCode atividade tooallow objeto erros de nível toobe toohello back retornado mecanismo de sincronização.
  * Olá atualizada SAP6 e SAP6User modelos toouse Olá novo nível de erro funcionalidade do objeto.
* Conector do Lotus Domino:
  * Para exportar, é necessário um certificador por catálogo de endereços. Você pode agora usar Olá mesmo senha para todos os certifiers toomake Olá gerenciamento mais fácil.

**Problemas corrigidos:**

* Conector LDAP Genérico:
  * Para o IBM Tivoli DS, alguns atributos de referência não foram detectados corretamente.
  * Para abrir LDAP durante a importação de delta, espaços em branco no início de saudação e no final de cadeias de caracteres foram truncados.
  * Para Novell e NetIQ, uma exportação que moveu um objeto entre OUs/contêineres e em Olá a mesma hora objeto renomeado Olá falhou.
* Conector dos Serviços Web:
  * Se o serviço web de saudação tiver vários pontos de extremidade para a mesma associação, em seguida, hello conector não corretamente descobriu esses pontos de extremidade.
* Conector do Lotus Domino:
  * Uma exportação de saudação fullName atributo tooa mail no banco de dados não funcionou.
  * Uma exportação qual membro adicionado e removido de um grupo só exportado Olá adicionou membros.
  * Se um documento de notas é inválido (Olá atributo isValid definido toofalse), Olá a falha do conector.

## <a name="older-releases"></a>Versões mais antigas
Antes de março de 2016, Olá conectores foram lançados como tópicos de suporte.

**LDAP Genérico**

* [KB3078617](https://support.microsoft.com/kb/3078617) – 1.0.0597, setembro de 2015
* [KB3044896](https://support.microsoft.com/kb/3044896) – 1.0.0549, março de 2015
* [KB3031009](https://support.microsoft.com/kb/3031009) – 1.0.0534, janeiro de 2015
* [KB3008177](https://support.microsoft.com/kb/3008177) – 1.0.0419, setembro de 2014
* [KB2936070](https://support.microsoft.com/kb/2936070) – 4.3.1082, março de 2014

**Serviços Web**

* [KB3008178](https://support.microsoft.com/kb/3008178) – 1.0.0419, setembro de 2014

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) – 1.0.0419, setembro de 2014

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) – 1.0.0597, setembro de 2015
* [KB3044895](https://support.microsoft.com/kb/3044895) – 1.0.0549, março de 2015
* [KB2977286](https://support.microsoft.com/kb/2977286) – 5.3.0712, agosto de 2014
* [KB2932635](https://support.microsoft.com/kb/2932635) – 5.3.1003, fevereiro de 2014  
* [KB2899874](https://support.microsoft.com/kb/2899874) – 5.3.0721, outubro de 2013
* [KB2875551](https://support.microsoft.com/kb/2875551) – 5.3.0534, agosto de 2013

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
