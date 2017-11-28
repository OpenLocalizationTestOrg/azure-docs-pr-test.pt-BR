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
# <a name="connector-version-release-history"></a><span data-ttu-id="9d46e-103">Histórico de lançamento de versão do conector</span><span class="sxs-lookup"><span data-stu-id="9d46e-103">Connector Version Release History</span></span>
<span data-ttu-id="9d46e-104">Olá conectores para o Forefront Identity Manager (FIM) e o Microsoft Identity Manager (MIM) são atualizados com frequência.</span><span class="sxs-lookup"><span data-stu-id="9d46e-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="9d46e-105">Este tópico é somente para FIM e MIM.</span><span class="sxs-lookup"><span data-stu-id="9d46e-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="9d46e-106">Esses conectores não são suportados para instalação no Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9d46e-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="9d46e-107">Conectores lançados pré-instaladas em AADConnect ao atualizar toospecified compilação.</span><span class="sxs-lookup"><span data-stu-id="9d46e-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="9d46e-108">Este tópico lista todas as versões do hello conectores que foram lançadas.</span><span class="sxs-lookup"><span data-stu-id="9d46e-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="9d46e-109">Links relacionados:</span><span class="sxs-lookup"><span data-stu-id="9d46e-109">Related links:</span></span>

* [<span data-ttu-id="9d46e-110">Baixar os Conectores mais recentes</span><span class="sxs-lookup"><span data-stu-id="9d46e-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="9d46e-111">[Conector LDAP Genérico](active-directory-aadconnectsync-connector-genericldap.md)</span><span class="sxs-lookup"><span data-stu-id="9d46e-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="9d46e-112">[Conector do SQL Genérico](active-directory-aadconnectsync-connector-genericsql.md)</span><span class="sxs-lookup"><span data-stu-id="9d46e-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="9d46e-113">[Conector dos Serviços Web](http://go.microsoft.com/fwlink/?LinkID=226245)</span><span class="sxs-lookup"><span data-stu-id="9d46e-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="9d46e-114">[Conector do PowerShell](active-directory-aadconnectsync-connector-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="9d46e-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="9d46e-115">[Conector do Lotus Domino](active-directory-aadconnectsync-connector-domino.md)</span><span class="sxs-lookup"><span data-stu-id="9d46e-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="9d46e-116">1.1.604.0 (AADConnect versão pendente)</span><span class="sxs-lookup"><span data-stu-id="9d46e-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="9d46e-117">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-117">Fixed issues:</span></span>

* <span data-ttu-id="9d46e-118">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-118">Generic Web Services:</span></span>
  * <span data-ttu-id="9d46e-119">Correção de um problema que estava impedindo um projeto SOAP de ser criado quando havia dois ou mais pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9d46e-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="9d46e-120">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-120">Generic SQL:</span></span>
  * <span data-ttu-id="9d46e-121">Na operação de saudação da importação Olá GSQL foi não converter tempo corretamente, quando salvo tooconnector espaço.</span><span class="sxs-lookup"><span data-stu-id="9d46e-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="9d46e-122">Olá formato de data e hora padrão para o espaço do conector de saudação GSQL foi alterado de 'AAAA-MM-dd: ssZ' too'yyyy-MM-dd: ssZ '.</span><span class="sxs-lookup"><span data-stu-id="9d46e-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="9d46e-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="9d46e-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="9d46e-124">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-124">Fixed issues:</span></span>

* <span data-ttu-id="9d46e-125">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-125">Generic Web Services:</span></span>
  * <span data-ttu-id="9d46e-126">ferramenta de como Wsconfig Olá não converteu corretamente matriz Json de saudação de "solicitação de exemplo" para o método de serviço REST hello.</span><span class="sxs-lookup"><span data-stu-id="9d46e-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="9d46e-127">Isso causava problemas com a serialização essa matriz Json para solicitação REST hello.</span><span class="sxs-lookup"><span data-stu-id="9d46e-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="9d46e-128">A Ferramenta de Configuração do Conector do Serviço Web não dá suporte ao uso de símbolos de espaço em nomes de atributo JSON</span><span class="sxs-lookup"><span data-stu-id="9d46e-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="9d46e-129">Um padrão de substituição pode ser adicionado manualmente toohello WSConfigTool.exe.config arquivo, por exemplo```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="9d46e-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="9d46e-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="9d46e-130">Lotus Notes:</span></span>
  * <span data-ttu-id="9d46e-131">Olá quando a opção **permitir certifiers personalizadas para as unidades organizacionais/organização** está desabilitado Olá conector falhar durante a exportação (atualização) depois que todos os atributos de fluxo de exportação hello serão exportado tooDomino, mas no tempo de saudação do Exportar um KeyNotFoundException é retornado tooSync.</span><span class="sxs-lookup"><span data-stu-id="9d46e-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="9d46e-132">Isso acontece porque Olá renomear operação falhar quando ele tenta toochange DN (atributo de nome de usuário) alterando um dos atributos de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="9d46e-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="9d46e-133">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="9d46e-133">LastName</span></span>
      - <span data-ttu-id="9d46e-134">Nome</span><span class="sxs-lookup"><span data-stu-id="9d46e-134">FirstName</span></span>
      - <span data-ttu-id="9d46e-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="9d46e-135">MiddleInitial</span></span>
      - <span data-ttu-id="9d46e-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="9d46e-136">AltFullName</span></span>
      - <span data-ttu-id="9d46e-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="9d46e-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="9d46e-138">ou</span><span class="sxs-lookup"><span data-stu-id="9d46e-138">ou</span></span>
      - <span data-ttu-id="9d46e-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="9d46e-139">altcommonname</span></span>

  * <span data-ttu-id="9d46e-140">Quando a opção **Permitir certificadores personalizados para a organização/as unidades organizacionais** está habilitada, mas os certificadores necessários ainda estão vazios, ocorre uma KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="9d46e-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="9d46e-141">Melhorias:</span><span class="sxs-lookup"><span data-stu-id="9d46e-141">Enhancements:</span></span>

* <span data-ttu-id="9d46e-142">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-142">Generic SQL:</span></span>
  * <span data-ttu-id="9d46e-143">**Cenário: reprojetado implementado:** recurso "*"</span><span class="sxs-lookup"><span data-stu-id="9d46e-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="9d46e-144">**Descrição da solução:** abordagem alterada para a [manipulação de atributos de referência de vários valores](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="9d46e-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="9d46e-145">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-145">Fixed issues:</span></span>

* <span data-ttu-id="9d46e-146">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-146">Generic Web Services:</span></span>
  * <span data-ttu-id="9d46e-147">Não será possível importar a configuração do servidor se houver um Conector WebService</span><span class="sxs-lookup"><span data-stu-id="9d46e-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="9d46e-148">O Conector WebService não está funcionando com vários Serviços Web</span><span class="sxs-lookup"><span data-stu-id="9d46e-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="9d46e-149">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-149">Generic SQL:</span></span>
  * <span data-ttu-id="9d46e-150">Nenhum tipo de objeto é listado para o atributo de referência de valor único</span><span class="sxs-lookup"><span data-stu-id="9d46e-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="9d46e-151">A importação delta na estratégia de Controle de Alterações exclui o objeto quando o valor é removido da tabela de vários valores</span><span class="sxs-lookup"><span data-stu-id="9d46e-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="9d46e-152">OverflowException no conector GSQL com DB2 no AS/400</span><span class="sxs-lookup"><span data-stu-id="9d46e-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="9d46e-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="9d46e-153">Lotus:</span></span>
  * <span data-ttu-id="9d46e-154">Opção adicional tooenable\disable pesquisando UOs antes de abrir a página GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="9d46e-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="9d46e-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="9d46e-155">1.1.443.0</span></span>

<span data-ttu-id="9d46e-156">Lançamento: março de 2017</span><span class="sxs-lookup"><span data-stu-id="9d46e-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="9d46e-157">Melhorias</span><span class="sxs-lookup"><span data-stu-id="9d46e-157">Enhancements</span></span>

* <span data-ttu-id="9d46e-158">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-158">Generic SQL:</span></span></br><span data-ttu-id="9d46e-159">
  **Cenário sintomas:** é uma limitação conhecida com hello conector do SQL onde podemos permitir somente um tipo de objeto de tooone de referência e exigem uma referência cruzada com membros.</span><span class="sxs-lookup"><span data-stu-id="9d46e-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="9d46e-160">
**Descrição da solução:** na etapa de processamento de saudação para referências foram "*" opção for escolhida, todas as combinações de tipos de objeto serão retornadas o mecanismo de sincronização toohello voltar.</span><span class="sxs-lookup"><span data-stu-id="9d46e-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="9d46e-161">Isso cria vários espaços reservados</span><span class="sxs-lookup"><span data-stu-id="9d46e-161">This will create many placeholders</span></span>
- <span data-ttu-id="9d46e-162">É necessário toomake se Olá de nomenclatura é exclusivo entre tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="9d46e-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="9d46e-163">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-163">Generic LDAP:</span></span></br><span data-ttu-id="9d46e-164">
 **Cenário:** quando apenas alguns contêineres são selecionados na partição específica, em seguida, pesquisa Olá ainda será feita na partição inteira.</span><span class="sxs-lookup"><span data-stu-id="9d46e-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="9d46e-165">O específico será filtrado pelo serviço de sincronização, mas não pelo MA que pode causar degradação do desempenho.</span><span class="sxs-lookup"><span data-stu-id="9d46e-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="9d46e-166">**Descrição da solução:** toomake de código do conector alterado GLDAP possível passar por todos os contêineres e pesquisar objetos em cada um deles, em vez de procurar na partição inteira hello.</span><span class="sxs-lookup"><span data-stu-id="9d46e-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="9d46e-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="9d46e-167">Lotus Domino:</span></span>

  <span data-ttu-id="9d46e-168">**Cenário:** o suporte para exclusão de email Domino para a remoção de pessoa durante uma exportação.</span><span class="sxs-lookup"><span data-stu-id="9d46e-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="9d46e-169">
  **Solução:** suporte para exclusão de email configurável para a remoção de pessoa durante uma exportação.</span><span class="sxs-lookup"><span data-stu-id="9d46e-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="9d46e-170">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-170">Fixed issues:</span></span>
* <span data-ttu-id="9d46e-171">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="9d46e-171">Generic Web Services:</span></span>
 * <span data-ttu-id="9d46e-172">Ao alterar a URL do serviço de saudação padrão como SAP wsconfig projetos por meio da ferramenta de configuração do serviço Web, em seguida, Olá erro a seguir ocorre: não foi possível localizar uma parte do caminho de saudação</span><span class="sxs-lookup"><span data-stu-id="9d46e-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="9d46e-173">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-173">Generic LDAP:</span></span>
 * <span data-ttu-id="9d46e-174">O conector de GLDAP não verá todos os atributos no AD LDS</span><span class="sxs-lookup"><span data-stu-id="9d46e-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="9d46e-175">Assistente quebras quando nenhum atributo UPN é detectado do esquema de diretório LDAP Olá</span><span class="sxs-lookup"><span data-stu-id="9d46e-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="9d46e-176">Quando o atributo de "objectclass" não está selecionado, há falha na importação Delta com erros de descoberta não presentes durante a importação completa</span><span class="sxs-lookup"><span data-stu-id="9d46e-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="9d46e-177">Uma página de configuração "Configurar partições e hierarquias", não mostra todos os objetos que tipo é partição toohello igual para servidores Novel Olá genérico</span><span class="sxs-lookup"><span data-stu-id="9d46e-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="9d46e-178">LDAP MA.</span><span class="sxs-lookup"><span data-stu-id="9d46e-178">LDAP MA.</span></span> <span data-ttu-id="9d46e-179">Eles exibem apenas objetos de partição RootDSE.</span><span class="sxs-lookup"><span data-stu-id="9d46e-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="9d46e-180">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-180">Generic SQL:</span></span>
 * <span data-ttu-id="9d46e-181">Fixo para bug de atributo com multivalores de importação Delta de marca d'água de SQL não importado</span><span class="sxs-lookup"><span data-stu-id="9d46e-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="9d46e-182">Ao exportar valores excluídos/adicionados de atributo com multivalores, eles não são excluídos/adicionados na fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="9d46e-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="9d46e-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="9d46e-183">Lotus Notes:</span></span>
 * <span data-ttu-id="9d46e-184">Um campo específico "Nome completo" é mostrado no metaverso Olá corretamente no entanto quando exportar tooNotes Olá valor para o atributo de saudação é nulo ou vazio.</span><span class="sxs-lookup"><span data-stu-id="9d46e-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="9d46e-185">Fixo para o erro de certificador de duplicata</span><span class="sxs-lookup"><span data-stu-id="9d46e-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="9d46e-186">Quando Olá objeto sem nenhum dado for selecionado no hello Lotus Domino conector com outros objetos que recebemos erro de descoberta de saudação ao executar importação completa.</span><span class="sxs-lookup"><span data-stu-id="9d46e-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="9d46e-187">Quando a importação de Delta é sendo executar em Olá Lotus Domino conector, final Olá Olá que execute, Microsoft.IdentityManagement.MA.LotusDomino.Service.exe serviço às vezes, retorna um erro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d46e-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="9d46e-188">Associação de grupo geral funciona bem e é mantida, exceto durante a execução Olá exportação tootry tooremove um usuário da associação mostra como êxito com uma atualização, mas o usuário hello, na verdade, não é removido da associação em Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="9d46e-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="9d46e-189">Um modo de toochoose oportunidade de exportação como "Acrescentar o Item na parte inferior" foi adicionado na configuração de GUI do Lotus MA tooappend novos itens na parte inferior durante a exportação de saudação para atributos com valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="9d46e-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="9d46e-190">Conector adicionará Olá necessário arquivo de saudação toodelete lógica da pasta de emails de saudação e ID do cofre.</span><span class="sxs-lookup"><span data-stu-id="9d46e-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="9d46e-191">Exclua a associação que não estiver funcionando para membro NAB cruzado.</span><span class="sxs-lookup"><span data-stu-id="9d46e-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="9d46e-192">Os valores devem ser excluídos com êxito do atributo de multivalores</span><span class="sxs-lookup"><span data-stu-id="9d46e-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="9d46e-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="9d46e-193">1.1.117.0</span></span>
<span data-ttu-id="9d46e-194">Lançamento: março de 2016</span><span class="sxs-lookup"><span data-stu-id="9d46e-194">Released: 2016 March</span></span>

<span data-ttu-id="9d46e-195">**Novo Conector**</span><span class="sxs-lookup"><span data-stu-id="9d46e-195">**New Connector**</span></span>  
<span data-ttu-id="9d46e-196">Versão da saudação inicial [conector do SQL genérico](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="9d46e-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="9d46e-197">**Novos recursos:**</span><span class="sxs-lookup"><span data-stu-id="9d46e-197">**New features:**</span></span>

* <span data-ttu-id="9d46e-198">Conector LDAP Genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="9d46e-199">Adicionado suporte para importação delta com o Isode.</span><span class="sxs-lookup"><span data-stu-id="9d46e-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="9d46e-200">Conector dos Serviços Web:</span><span class="sxs-lookup"><span data-stu-id="9d46e-200">Web Services Connector:</span></span>
  * <span data-ttu-id="9d46e-201">Olá atualizada csEntryChangeResult atividade e setImportErrorCode atividade tooallow objeto erros de nível toobe toohello back retornado mecanismo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="9d46e-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="9d46e-202">Olá atualizada SAP6 e SAP6User modelos toouse Olá novo nível de erro funcionalidade do objeto.</span><span class="sxs-lookup"><span data-stu-id="9d46e-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="9d46e-203">Conector do Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="9d46e-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="9d46e-204">Para exportar, é necessário um certificador por catálogo de endereços.</span><span class="sxs-lookup"><span data-stu-id="9d46e-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="9d46e-205">Você pode agora usar Olá mesmo senha para todos os certifiers toomake Olá gerenciamento mais fácil.</span><span class="sxs-lookup"><span data-stu-id="9d46e-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="9d46e-206">**Problemas corrigidos:**</span><span class="sxs-lookup"><span data-stu-id="9d46e-206">**Fixed issues:**</span></span>

* <span data-ttu-id="9d46e-207">Conector LDAP Genérico:</span><span class="sxs-lookup"><span data-stu-id="9d46e-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="9d46e-208">Para o IBM Tivoli DS, alguns atributos de referência não foram detectados corretamente.</span><span class="sxs-lookup"><span data-stu-id="9d46e-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="9d46e-209">Para abrir LDAP durante a importação de delta, espaços em branco no início de saudação e no final de cadeias de caracteres foram truncados.</span><span class="sxs-lookup"><span data-stu-id="9d46e-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="9d46e-210">Para Novell e NetIQ, uma exportação que moveu um objeto entre OUs/contêineres e em Olá a mesma hora objeto renomeado Olá falhou.</span><span class="sxs-lookup"><span data-stu-id="9d46e-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="9d46e-211">Conector dos Serviços Web:</span><span class="sxs-lookup"><span data-stu-id="9d46e-211">Web Services Connector:</span></span>
  * <span data-ttu-id="9d46e-212">Se o serviço web de saudação tiver vários pontos de extremidade para a mesma associação, em seguida, hello conector não corretamente descobriu esses pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9d46e-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="9d46e-213">Conector do Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="9d46e-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="9d46e-214">Uma exportação de saudação fullName atributo tooa mail no banco de dados não funcionou.</span><span class="sxs-lookup"><span data-stu-id="9d46e-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="9d46e-215">Uma exportação qual membro adicionado e removido de um grupo só exportado Olá adicionou membros.</span><span class="sxs-lookup"><span data-stu-id="9d46e-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="9d46e-216">Se um documento de notas é inválido (Olá atributo isValid definido toofalse), Olá a falha do conector.</span><span class="sxs-lookup"><span data-stu-id="9d46e-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="9d46e-217">Versões mais antigas</span><span class="sxs-lookup"><span data-stu-id="9d46e-217">Older releases</span></span>
<span data-ttu-id="9d46e-218">Antes de março de 2016, Olá conectores foram lançados como tópicos de suporte.</span><span class="sxs-lookup"><span data-stu-id="9d46e-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="9d46e-219">**LDAP Genérico**</span><span class="sxs-lookup"><span data-stu-id="9d46e-219">**Generic LDAP**</span></span>

* <span data-ttu-id="9d46e-220">[KB3078617](https://support.microsoft.com/kb/3078617) – 1.0.0597, setembro de 2015</span><span class="sxs-lookup"><span data-stu-id="9d46e-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="9d46e-221">[KB3044896](https://support.microsoft.com/kb/3044896) – 1.0.0549, março de 2015</span><span class="sxs-lookup"><span data-stu-id="9d46e-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="9d46e-222">[KB3031009](https://support.microsoft.com/kb/3031009) – 1.0.0534, janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="9d46e-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="9d46e-223">[KB3008177](https://support.microsoft.com/kb/3008177) – 1.0.0419, setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="9d46e-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="9d46e-224">[KB2936070](https://support.microsoft.com/kb/2936070) – 4.3.1082, março de 2014</span><span class="sxs-lookup"><span data-stu-id="9d46e-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="9d46e-225">**Serviços Web**</span><span class="sxs-lookup"><span data-stu-id="9d46e-225">**WebServices**</span></span>

* <span data-ttu-id="9d46e-226">[KB3008178](https://support.microsoft.com/kb/3008178) – 1.0.0419, setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="9d46e-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="9d46e-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9d46e-227">**PowerShell**</span></span>

* <span data-ttu-id="9d46e-228">[KB3008179](https://support.microsoft.com/kb/3008179) – 1.0.0419, setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="9d46e-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="9d46e-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="9d46e-229">**Lotus Domino**</span></span>

* <span data-ttu-id="9d46e-230">[KB3096533](https://support.microsoft.com/kb/3096533) – 1.0.0597, setembro de 2015</span><span class="sxs-lookup"><span data-stu-id="9d46e-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="9d46e-231">[KB3044895](https://support.microsoft.com/kb/3044895) – 1.0.0549, março de 2015</span><span class="sxs-lookup"><span data-stu-id="9d46e-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="9d46e-232">[KB2977286](https://support.microsoft.com/kb/2977286) – 5.3.0712, agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="9d46e-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="9d46e-233">[KB2932635](https://support.microsoft.com/kb/2932635) – 5.3.1003, fevereiro de 2014</span><span class="sxs-lookup"><span data-stu-id="9d46e-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="9d46e-234">[KB2899874](https://support.microsoft.com/kb/2899874) – 5.3.0721, outubro de 2013</span><span class="sxs-lookup"><span data-stu-id="9d46e-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="9d46e-235">[KB2875551](https://support.microsoft.com/kb/2875551) – 5.3.0534, agosto de 2013</span><span class="sxs-lookup"><span data-stu-id="9d46e-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d46e-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d46e-236">Next steps</span></span>
<span data-ttu-id="9d46e-237">Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.</span><span class="sxs-lookup"><span data-stu-id="9d46e-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9d46e-238">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9d46e-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
