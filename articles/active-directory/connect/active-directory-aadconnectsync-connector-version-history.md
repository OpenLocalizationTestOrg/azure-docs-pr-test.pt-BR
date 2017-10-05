---
title: "Histórico de lançamento de versão do conector | Microsoft Docs"
description: "Este tópico lista todas as versões dos Conectores do FIM (Forefront Identity Manager) e MIM (Microsoft Identity Manager)"
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
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="c4799-103">Histórico de lançamento de versão do conector</span><span class="sxs-lookup"><span data-stu-id="c4799-103">Connector Version Release History</span></span>
<span data-ttu-id="c4799-104">Os Conectores do FIM (Forefront Identity Manager) e MIM (Microsoft Identity Manager) são atualizados com frequência.</span><span class="sxs-lookup"><span data-stu-id="c4799-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="c4799-105">Este tópico é somente para FIM e MIM.</span><span class="sxs-lookup"><span data-stu-id="c4799-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="c4799-106">Esses conectores não são suportados para instalação no Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c4799-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="c4799-107">Os conectores liberados são pré-instalados no AADConnect durante o upgrade para o Build especificado.</span><span class="sxs-lookup"><span data-stu-id="c4799-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="c4799-108">Este tópico lista todas as versões dos conectores que foram lançadas.</span><span class="sxs-lookup"><span data-stu-id="c4799-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="c4799-109">Links relacionados:</span><span class="sxs-lookup"><span data-stu-id="c4799-109">Related links:</span></span>

* [<span data-ttu-id="c4799-110">Baixar os Conectores mais recentes</span><span class="sxs-lookup"><span data-stu-id="c4799-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="c4799-111">[Conector LDAP Genérico](active-directory-aadconnectsync-connector-genericldap.md)</span><span class="sxs-lookup"><span data-stu-id="c4799-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="c4799-112">[Conector do SQL Genérico](active-directory-aadconnectsync-connector-genericsql.md)</span><span class="sxs-lookup"><span data-stu-id="c4799-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="c4799-113">[Conector dos Serviços Web](http://go.microsoft.com/fwlink/?LinkID=226245)</span><span class="sxs-lookup"><span data-stu-id="c4799-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="c4799-114">[Conector do PowerShell](active-directory-aadconnectsync-connector-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c4799-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="c4799-115">[Conector do Lotus Domino](active-directory-aadconnectsync-connector-domino.md)</span><span class="sxs-lookup"><span data-stu-id="c4799-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="c4799-116">1.1.604.0 (AADConnect versão pendente)</span><span class="sxs-lookup"><span data-stu-id="c4799-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="c4799-117">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="c4799-117">Fixed issues:</span></span>

* <span data-ttu-id="c4799-118">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="c4799-118">Generic Web Services:</span></span>
  * <span data-ttu-id="c4799-119">Correção de um problema que estava impedindo um projeto SOAP de ser criado quando havia dois ou mais pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="c4799-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="c4799-120">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-120">Generic SQL:</span></span>
  * <span data-ttu-id="c4799-121">Na operação de importação, o GSQL não estava convertendo o tempo corretamente, quando salvo no espaço do conector.</span><span class="sxs-lookup"><span data-stu-id="c4799-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="c4799-122">O formato de data e hora padrão para o espaço do conector do GSQL foi alterado de "aaaa-MM-dd hh:mm:ssZ'' para "aaaa-MM-dd HH:mm:ssZ'.</span><span class="sxs-lookup"><span data-stu-id="c4799-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="c4799-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="c4799-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="c4799-124">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="c4799-124">Fixed issues:</span></span>

* <span data-ttu-id="c4799-125">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="c4799-125">Generic Web Services:</span></span>
  * <span data-ttu-id="c4799-126">A ferramenta Wsconfig não converteu corretamente a matriz JSON de "solicitação de exemplo" para o método de serviço REST.</span><span class="sxs-lookup"><span data-stu-id="c4799-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="c4799-127">Isso causou problemas com a serialização dessa matriz Json para a solicitação REST.</span><span class="sxs-lookup"><span data-stu-id="c4799-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="c4799-128">A Ferramenta de Configuração do Conector do Serviço Web não dá suporte ao uso de símbolos de espaço em nomes de atributo JSON</span><span class="sxs-lookup"><span data-stu-id="c4799-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="c4799-129">Um padrão de substituição pode ser adicionado manualmente ao arquivo WSConfigTool.exe.config, por exemplo ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="c4799-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="c4799-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="c4799-130">Lotus Notes:</span></span>
  * <span data-ttu-id="c4799-131">Quando a opção **Permitir certificadores personalizados para a organização/as unidades organizacionais** está desabilitada, o conector falha durante a exportação (Atualização) Após o fluxo de exportação, todos os atributos são exportados para o Domino mas, no momento da exportação, uma KeyNotFoundException é retornada para Sincronização.</span><span class="sxs-lookup"><span data-stu-id="c4799-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="c4799-132">Isso acontece porque a operação de renomeação falha ao tentar alterar o DN (atributo UserName) alterando um dos atributos abaixo:</span><span class="sxs-lookup"><span data-stu-id="c4799-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="c4799-133">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="c4799-133">LastName</span></span>
      - <span data-ttu-id="c4799-134">Nome</span><span class="sxs-lookup"><span data-stu-id="c4799-134">FirstName</span></span>
      - <span data-ttu-id="c4799-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="c4799-135">MiddleInitial</span></span>
      - <span data-ttu-id="c4799-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="c4799-136">AltFullName</span></span>
      - <span data-ttu-id="c4799-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="c4799-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="c4799-138">ou</span><span class="sxs-lookup"><span data-stu-id="c4799-138">ou</span></span>
      - <span data-ttu-id="c4799-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="c4799-139">altcommonname</span></span>

  * <span data-ttu-id="c4799-140">Quando a opção **Permitir certificadores personalizados para a organização/as unidades organizacionais** está habilitada, mas os certificadores necessários ainda estão vazios, ocorre uma KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="c4799-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="c4799-141">Melhorias:</span><span class="sxs-lookup"><span data-stu-id="c4799-141">Enhancements:</span></span>

* <span data-ttu-id="c4799-142">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-142">Generic SQL:</span></span>
  * <span data-ttu-id="c4799-143">**Cenário: reprojetado implementado:** recurso "*"</span><span class="sxs-lookup"><span data-stu-id="c4799-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="c4799-144">**Descrição da solução:** abordagem alterada para a [manipulação de atributos de referência de vários valores](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="c4799-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="c4799-145">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="c4799-145">Fixed issues:</span></span>

* <span data-ttu-id="c4799-146">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="c4799-146">Generic Web Services:</span></span>
  * <span data-ttu-id="c4799-147">Não será possível importar a configuração do servidor se houver um Conector WebService</span><span class="sxs-lookup"><span data-stu-id="c4799-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="c4799-148">O Conector WebService não está funcionando com vários Serviços Web</span><span class="sxs-lookup"><span data-stu-id="c4799-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="c4799-149">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-149">Generic SQL:</span></span>
  * <span data-ttu-id="c4799-150">Nenhum tipo de objeto é listado para o atributo de referência de valor único</span><span class="sxs-lookup"><span data-stu-id="c4799-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="c4799-151">A importação delta na estratégia de Controle de Alterações exclui o objeto quando o valor é removido da tabela de vários valores</span><span class="sxs-lookup"><span data-stu-id="c4799-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="c4799-152">OverflowException no conector GSQL com DB2 no AS/400</span><span class="sxs-lookup"><span data-stu-id="c4799-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="c4799-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="c4799-153">Lotus:</span></span>
  * <span data-ttu-id="c4799-154">Adicionada a opção de habilitar/desabilitar a pesquisa de UOs antes de abrir a página GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="c4799-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="c4799-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="c4799-155">1.1.443.0</span></span>

<span data-ttu-id="c4799-156">Lançamento: março de 2017</span><span class="sxs-lookup"><span data-stu-id="c4799-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="c4799-157">Melhorias</span><span class="sxs-lookup"><span data-stu-id="c4799-157">Enhancements</span></span>

* <span data-ttu-id="c4799-158">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-158">Generic SQL:</span></span></br><span data-ttu-id="c4799-159">
  **Sintomas de cenário:** são uma limitação conhecida com o conector do SQL onde podemos permitir somente uma referência a um tipo de objeto e exigir uma referência cruzada com membros.</span><span class="sxs-lookup"><span data-stu-id="c4799-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="c4799-160">
**Descrição da solução:** na etapa de processamento de referências onde a opção "*" é escolhida, todas as combinações de tipos de objeto são retornadas para o mecanismo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="c4799-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="c4799-161">Isso cria vários espaços reservados</span><span class="sxs-lookup"><span data-stu-id="c4799-161">This will create many placeholders</span></span>
- <span data-ttu-id="c4799-162">Isso é necessário para garantir que o nome seja exclusivo entre tipos de objetos cruzados.</span><span class="sxs-lookup"><span data-stu-id="c4799-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="c4799-163">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-163">Generic LDAP:</span></span></br><span data-ttu-id="c4799-164">
 **Cenário:** quando apenas alguns contêineres são selecionados na partição específica e a pesquisa ainda será realizada na partição inteira.</span><span class="sxs-lookup"><span data-stu-id="c4799-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="c4799-165">O específico será filtrado pelo serviço de sincronização, mas não pelo MA que pode causar degradação do desempenho.</span><span class="sxs-lookup"><span data-stu-id="c4799-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="c4799-166">**Descrição de solução:**  o código do conector GLDAP é modificado para passar por todos os contêineres e objetos de pesquisa em cada um deles, em vez de pesquisar na partição inteira.</span><span class="sxs-lookup"><span data-stu-id="c4799-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="c4799-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="c4799-167">Lotus Domino:</span></span>

  <span data-ttu-id="c4799-168">**Cenário:** o suporte para exclusão de email Domino para a remoção de pessoa durante uma exportação.</span><span class="sxs-lookup"><span data-stu-id="c4799-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="c4799-169">
  **Solução:** suporte para exclusão de email configurável para a remoção de pessoa durante uma exportação.</span><span class="sxs-lookup"><span data-stu-id="c4799-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="c4799-170">Problemas corrigidos:</span><span class="sxs-lookup"><span data-stu-id="c4799-170">Fixed issues:</span></span>
* <span data-ttu-id="c4799-171">Serviços Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="c4799-171">Generic Web Services:</span></span>
 * <span data-ttu-id="c4799-172">Ao alterar a URL do serviço nos projetos wsconfig SAP padrão usando a ferramenta de configuração do serviço da Web, aparece o seguinte erro: não foi possível localizar uma parte do caminho</span><span class="sxs-lookup"><span data-stu-id="c4799-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="c4799-173">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-173">Generic LDAP:</span></span>
 * <span data-ttu-id="c4799-174">O conector de GLDAP não verá todos os atributos no AD LDS</span><span class="sxs-lookup"><span data-stu-id="c4799-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="c4799-175">Quebra de assistente quando não é detectado nenhum atributo UPN do esquema de diretório LDAP</span><span class="sxs-lookup"><span data-stu-id="c4799-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="c4799-176">Quando o atributo de "objectclass" não está selecionado, há falha na importação Delta com erros de descoberta não presentes durante a importação completa</span><span class="sxs-lookup"><span data-stu-id="c4799-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="c4799-177">Uma página de configuração "Configurar partições e hierarquias", não exibe todos os objetos cujos tipos são iguais à partição para servidores Novel no Genérico</span><span class="sxs-lookup"><span data-stu-id="c4799-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="c4799-178">LDAP MA.</span><span class="sxs-lookup"><span data-stu-id="c4799-178">LDAP MA.</span></span> <span data-ttu-id="c4799-179">Eles exibem apenas objetos de partição RootDSE.</span><span class="sxs-lookup"><span data-stu-id="c4799-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="c4799-180">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-180">Generic SQL:</span></span>
 * <span data-ttu-id="c4799-181">Fixo para bug de atributo com multivalores de importação Delta de marca d'água de SQL não importado</span><span class="sxs-lookup"><span data-stu-id="c4799-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="c4799-182">Ao exportar valores excluídos/adicionados de atributo com multivalores, eles não são excluídos/adicionados na fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="c4799-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="c4799-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="c4799-183">Lotus Notes:</span></span>
 * <span data-ttu-id="c4799-184">Um campo específico "Nome completo" é mostrado corretamente no metaverso, no entanto, o valor do atributo se torna nulo ou vazio quando exportado para notas.</span><span class="sxs-lookup"><span data-stu-id="c4799-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="c4799-185">Fixo para o erro de certificador de duplicata</span><span class="sxs-lookup"><span data-stu-id="c4799-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="c4799-186">Quando o objeto sem dados é selecionado no conector Lotus Domino com outros objetos e, em seguida, recebemos o erro de descoberta ao executar a importação completa.</span><span class="sxs-lookup"><span data-stu-id="c4799-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="c4799-187">Às vezes, no final da execução da importação Delta no conector Lotus Domino, o serviço Microsoft.IdentityManagement.MA.LotusDomino.Service.exe retorna uma mensagem de erro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4799-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="c4799-188">O geral da associação do grupo funciona bem e é mantido, exceto ao executar a exportação para tentar remover um usuário da associação, apesar de exibir mensagem de êxito com uma atualização, o usuário não é removido da associação no Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="c4799-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="c4799-189">A oportunidade de escolher o modo de exportação como "Acrescentar item no final" foi adicionada na configuração de GUI do Lotus MA para acrescentar itens novos no final durante a exportação de atributos com multivalores.</span><span class="sxs-lookup"><span data-stu-id="c4799-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="c4799-190">O conector adicionará a lógica necessária para excluir o arquivo da pasta de email e o cofre de ID.</span><span class="sxs-lookup"><span data-stu-id="c4799-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="c4799-191">Exclua a associação que não estiver funcionando para membro NAB cruzado.</span><span class="sxs-lookup"><span data-stu-id="c4799-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="c4799-192">Os valores devem ser excluídos com êxito do atributo de multivalores</span><span class="sxs-lookup"><span data-stu-id="c4799-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="c4799-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="c4799-193">1.1.117.0</span></span>
<span data-ttu-id="c4799-194">Lançamento: março de 2016</span><span class="sxs-lookup"><span data-stu-id="c4799-194">Released: 2016 March</span></span>

<span data-ttu-id="c4799-195">**Novo Conector**</span><span class="sxs-lookup"><span data-stu-id="c4799-195">**New Connector**</span></span>  
<span data-ttu-id="c4799-196">Versão inicial do [Conector do SQL Genérico](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="c4799-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="c4799-197">**Novos recursos:**</span><span class="sxs-lookup"><span data-stu-id="c4799-197">**New features:**</span></span>

* <span data-ttu-id="c4799-198">Conector LDAP Genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="c4799-199">Adicionado suporte para importação delta com o Isode.</span><span class="sxs-lookup"><span data-stu-id="c4799-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="c4799-200">Conector dos Serviços Web:</span><span class="sxs-lookup"><span data-stu-id="c4799-200">Web Services Connector:</span></span>
  * <span data-ttu-id="c4799-201">Atualizadas as atividades csEntryChangeResult e setImportErrorCode para permitir que erros no nível de objeto sejam retornados para o mecanismo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="c4799-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="c4799-202">Atualizados os modelos SAP6 e SAP6User para usar a nova funcionalidade de erro no nível de objeto.</span><span class="sxs-lookup"><span data-stu-id="c4799-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="c4799-203">Conector do Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="c4799-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="c4799-204">Para exportar, é necessário um certificador por catálogo de endereços.</span><span class="sxs-lookup"><span data-stu-id="c4799-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="c4799-205">Agora é possível usar a mesma senha para todos os certificadores, a fim de facilitar o gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c4799-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="c4799-206">**Problemas corrigidos:**</span><span class="sxs-lookup"><span data-stu-id="c4799-206">**Fixed issues:**</span></span>

* <span data-ttu-id="c4799-207">Conector LDAP Genérico:</span><span class="sxs-lookup"><span data-stu-id="c4799-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="c4799-208">Para o IBM Tivoli DS, alguns atributos de referência não foram detectados corretamente.</span><span class="sxs-lookup"><span data-stu-id="c4799-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="c4799-209">Para o Open LDAP durante a importação delta, os espaços em branco no início e no final das cadeias de caracteres foram truncados.</span><span class="sxs-lookup"><span data-stu-id="c4799-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="c4799-210">Para o Novell e NetIQ, houve falha em uma exportação que movia um objeto entre UOs/contêineres e ao mesmo tempo renomeava o objeto.</span><span class="sxs-lookup"><span data-stu-id="c4799-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="c4799-211">Conector dos Serviços Web:</span><span class="sxs-lookup"><span data-stu-id="c4799-211">Web Services Connector:</span></span>
  * <span data-ttu-id="c4799-212">Se o serviço Web tinha vários pontos de extremidade para a mesma associação, o conector não os descobriu corretamente.</span><span class="sxs-lookup"><span data-stu-id="c4799-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="c4799-213">Conector do Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="c4799-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="c4799-214">Uma exportação do atributo fullName para um banco de dados de entrada de email não funcionou.</span><span class="sxs-lookup"><span data-stu-id="c4799-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="c4799-215">Uma exportação que adicionava e removia um membro de um grupo exportou apenas os membros adicionados.</span><span class="sxs-lookup"><span data-stu-id="c4799-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="c4799-216">Se um Documento do Notes for inválido (o atributo isValid for definido como false), haverá uma falha do Conector.</span><span class="sxs-lookup"><span data-stu-id="c4799-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="c4799-217">Versões mais antigas</span><span class="sxs-lookup"><span data-stu-id="c4799-217">Older releases</span></span>
<span data-ttu-id="c4799-218">Antes de março de 2016, os Conectores foram liberados como tópicos de suporte.</span><span class="sxs-lookup"><span data-stu-id="c4799-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="c4799-219">**LDAP Genérico**</span><span class="sxs-lookup"><span data-stu-id="c4799-219">**Generic LDAP**</span></span>

* <span data-ttu-id="c4799-220">[KB3078617](https://support.microsoft.com/kb/3078617) – 1.0.0597, setembro de 2015</span><span class="sxs-lookup"><span data-stu-id="c4799-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="c4799-221">[KB3044896](https://support.microsoft.com/kb/3044896) – 1.0.0549, março de 2015</span><span class="sxs-lookup"><span data-stu-id="c4799-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="c4799-222">[KB3031009](https://support.microsoft.com/kb/3031009) – 1.0.0534, janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="c4799-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="c4799-223">[KB3008177](https://support.microsoft.com/kb/3008177) – 1.0.0419, setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="c4799-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="c4799-224">[KB2936070](https://support.microsoft.com/kb/2936070) – 4.3.1082, março de 2014</span><span class="sxs-lookup"><span data-stu-id="c4799-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="c4799-225">**Serviços Web**</span><span class="sxs-lookup"><span data-stu-id="c4799-225">**WebServices**</span></span>

* <span data-ttu-id="c4799-226">[KB3008178](https://support.microsoft.com/kb/3008178) – 1.0.0419, setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="c4799-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="c4799-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="c4799-227">**PowerShell**</span></span>

* <span data-ttu-id="c4799-228">[KB3008179](https://support.microsoft.com/kb/3008179) – 1.0.0419, setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="c4799-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="c4799-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="c4799-229">**Lotus Domino**</span></span>

* <span data-ttu-id="c4799-230">[KB3096533](https://support.microsoft.com/kb/3096533) – 1.0.0597, setembro de 2015</span><span class="sxs-lookup"><span data-stu-id="c4799-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="c4799-231">[KB3044895](https://support.microsoft.com/kb/3044895) – 1.0.0549, março de 2015</span><span class="sxs-lookup"><span data-stu-id="c4799-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="c4799-232">[KB2977286](https://support.microsoft.com/kb/2977286) – 5.3.0712, agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="c4799-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="c4799-233">[KB2932635](https://support.microsoft.com/kb/2932635) – 5.3.1003, fevereiro de 2014</span><span class="sxs-lookup"><span data-stu-id="c4799-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="c4799-234">[KB2899874](https://support.microsoft.com/kb/2899874) – 5.3.0721, outubro de 2013</span><span class="sxs-lookup"><span data-stu-id="c4799-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="c4799-235">[KB2875551](https://support.microsoft.com/kb/2875551) – 5.3.0534, agosto de 2013</span><span class="sxs-lookup"><span data-stu-id="c4799-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4799-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4799-236">Next steps</span></span>
<span data-ttu-id="c4799-237">Saiba mais sobre a configuração de [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="c4799-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="c4799-238">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c4799-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
