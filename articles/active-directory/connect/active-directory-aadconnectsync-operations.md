---
title: "Sincronização do Azure AD Connect: considerações e tarefas operacionais | Microsoft Docs"
description: "Este tópico descreve as tarefas operacionais para a sincronização do Azure AD Connect e como tooprepare para a operação neste componente."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Sincronização do Azure AD Connect: considerações e tarefas operacionais
Olá objetivo deste tópico é toodescribe as tarefas operacionais para a sincronização do Azure AD Connect.

## <a name="staging-mode"></a>Modo de preparo
O modo de teste pode ser usado para vários cenários, incluindo:

* Alta disponibilidade.
* Teste e implantação de novas alterações de configuração.
* Introduz um novo servidor e encerrar Olá antigo.

Com um servidor no modo de preparo, você pode fazer alterações toohello configuração e visualizar Olá alterações antes de você ativar o servidor de saudação. Ele também permite importação completa toorun e sincronização completa tooverify que todas as alterações são esperadas antes de fazer essas alterações em seu ambiente de produção.

Durante a instalação, você pode selecionar Olá server toobe em **modo de preparo**. Esta ação ativa de importação e sincronização de servidor de saudação, mas não executa qualquer exportações. Um servidor no modo de preparo não executa a sincronização de senha ou o write-back de senha, mesmo que esses recursos sejam selecionados durante a instalação. Quando você desabilita o modo de preparo, o servidor de saudação inicia a exportação, permite a sincronização de senha e permite que o write-back de senha.

Você ainda pode forçar uma exportação usando o Gerenciador de serviço de sincronização de saudação.

Um servidor no modo de preparo continua tooreceive alterações do Active Directory e o AD do Azure. Ele sempre tem uma cópia das alterações mais recentes hello e podem levar muito rápido sobre responsabilidades de saudação do outro servidor. Se você tornar o servidor primário de tooyour de alterações de configuração, é sua responsabilidade toomake Olá mesmo servidor toohello de alterações no modo de preparo.

Para aqueles com conhecimento das tecnologias mais antigas de sincronização, Olá modo de preparo é diferente porque o servidor de saudação tem seu próprio banco de dados do SQL. Essa arquitetura permite Olá modo servidor toobe localizado em um datacenter diferente de preparo.

### <a name="verify-hello-configuration-of-a-server"></a>Verificar a configuração de saudação de um servidor
tooapply esse método, siga estas etapas:

1. [Preparar](#prepare)
2. [Configuração](#configuration)
3. [Importar e sincronizar](#import-and-synchronize)
4. [Verificar](#verify)
5. [Servidor ativo do comutador](#switch-active-server)

#### <a name="prepare"></a>Preparar
1. Instalar o Azure AD Connect, selecione **modo de preparo**e desmarque **iniciar a sincronização** na última página Olá no Assistente de instalação de saudação. Este modo permite o mecanismo de sincronização de saudação toorun manualmente.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Logoff/logon logon e de saudação iniciar no menu, selecione **serviço de sincronização**.

#### <a name="configuration"></a>Configuração
Se você tiver feito alterações personalizadas toohello primária deseja toocompare Olá configuração e com hello servidor de preparo, em seguida, use [Documentador de configuração do Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>Importar e sincronizar
1. Selecione **conectores**, e selecione Olá primeiro conector com o tipo de saudação **serviços de domínio do Active Directory**. Clique em **Executar**, selecione **Importação completa** e **OK**. Siga estas etapas para todos os Conectores desse tipo.
2. Selecione Olá conector com o tipo **do Active Directory do Azure (Microsoft)**. Clique em **Executar**, selecione **Importação completa** e **OK**.
3. Certifique-se de guia Olá conectores ainda está selecionado. Para cada Conector com tipo **Active Directory Domain Services**, clique em **Executar**, selecione **Sincronização Delta** e **OK**.
4. Selecione Olá conector com o tipo **do Active Directory do Azure (Microsoft)**. Clique em **Executar**, selecione **Sincronização Delta** e **OK**.

Você tem agora exportação preparada altera tooAzure AD e AD local (se você estiver usando a implantação híbrida do Exchange). as próximas etapas Olá permitem tooinspect novidades sobre toochange antes de você realmente iniciar Olá exportar toohello diretórios.

#### <a name="verify"></a>Verificar
1. Inicie um prompt de comando e vá muito`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Executar: `csexport "Name of Connector" %temp%\export.xml /f:x` nome de saudação do hello conector pode ser encontrado no serviço de sincronização. Ele tem um too"contoso.com de nome semelhante – AAD" do AD do Azure.
3. Copie o script do PowerShell de saudação da seção Olá [CSAnalyzer](#appendix-csanalyzer) tooa arquivo chamado `csanalyzer.ps1`.
4. Abra uma janela do PowerShell e procurar toohello pasta em que você criou o script do PowerShell hello.
5. Execute: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. Agora você tem um arquivo chamado **processedusers1.csv** que pode ser examinado no Microsoft Excel. TooAzure toobe exportado de todas as alterações de teste AD são encontrados nesse arquivo.
7. Faça as alterações necessárias toohello dados ou a configuração e execute estas etapas novamente (importar e sincronizar e verifique se) até Olá alterações sobre toobe exportado são esperadas.

#### <a name="switch-active-server"></a>Servidor ativo do comutador
1. No servidor ativo no momento do hello, desative o servidor de saudação (DirSync/FIM/Azure AD Sync) para que ele não esteja exportando tooAzure AD ou defina-o no modo (Azure AD Connect) de preparo.
2. Execute o Assistente de instalação de saudação no servidor de saudação em **modo de preparo** e desabilitar **modo de preparo**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Recuperação de desastre
Parte do design de implementação de saudação é tooplan para quais toodo caso haja um desastre em que você perder o servidor de sincronização de saudação. Há diferentes modelos toouse e quais um toouse depende de vários fatores, incluindo:

* Qual é sua tolerância de não ser capaz de fazer alterações de tooobjects no AD do Azure durante o tempo de inatividade Olá?
* Se você usar a sincronização de senha, os usuários de saudação aceitar que tem senha antiga de saudação toouse no AD do Azure caso eles alteração-lo no local?
* Você tem uma dependência em operações em tempo real, como write-back de senha?

Dependendo da saudação respostas toothese perguntas e a política da sua organização, uma saudação estratégias a seguir pode ser implementada:

* Recriar quando necessário.
* Ter um servidor em espera reserva, conhecido como **modo de preparo**.
* Usar máquinas virtuais.

Se você não usar Olá SQL Express banco de dados interno, você também deve revisar Olá [alta disponibilidade do SQL](#sql-high-availability) seção.

### <a name="rebuild-when-needed"></a>Recriar quando necessário
Uma estratégia viável é tooplan para a recriação do servidor quando necessário. Geralmente, instalando Olá mecanismo de sincronização e Olá importação inicial e sincronização pode ser concluída dentro de algumas horas. Se não houver um servidor de reserva disponíveis, é possível tootemporarily usar um mecanismo de sincronização de saudação do domínio controlador toohost.

servidor do mecanismo de sincronização de saudação não armazenam qualquer estado sobre objetos Olá para que o banco de dados de saudação poderá ser reconstruído com dados de saudação no Active Directory e o AD do Azure. Olá **sourceAnchor** atributo é usado toojoin Olá objetos do local e Olá nuvem. Se você recriar Olá servidor com objetos locais existentes e Olá nuvem, em seguida, o mecanismo de sincronização de saudação corresponde a esses objetos juntos novamente na reinstalação. coisas Olá necessário toodocument e salvar são Olá alterações de configuração toohello server, como regras de sincronização e filtragem. Essas configurações personalizadas devem ser reaplicadas antes que você inicie a sincronização.

### <a name="have-a-spare-standby-server---staging-mode"></a>Ter um servidor em espera reserva - modo de preparo
Se você tiver um ambiente mais complexo, é recomendável ter um ou mais servidores em espera. Durante a instalação, você pode habilitar um toobe de servidor em **modo de preparo**.

Para obter mais informações, consulte [Modo de preparo](#staging-mode).

### <a name="use-virtual-machines"></a>Usar máquinas virtuais
Um método comum e com suporte é o mecanismo de sincronização de saudação toorun em uma máquina virtual. No caso de host Olá tem um problema, a imagem de Olá com o servidor do mecanismo de sincronização de saudação pode ser migrado tooanother server.

### <a name="sql-high-availability"></a>Alta disponibilidade do SQL
Se você não estiver usando o SQL Server Express que vem com o Azure AD Connect de saudação, alta disponibilidade para o SQL Server também deve ser considerada. soluções de alta disponibilidade Olá com suporte incluem o clustering de SQL e AOA (grupos de disponibilidade AlwaysOn). Soluções sem suporte incluem espelhamento.

Suporte para SQL AOA foi adicionado tooAzure AD Connect versão 1.1.524.0. Você deve habilitar o SQL AOA antes de instalar o Azure AD Connect. Durante a instalação, o Azure AD Connect detecta se a instância SQL Olá fornecida está habilitada para SQL AOA, ou não. Se SQL AOA estiver habilitado, o Azure AD Connect mais descobre se SQL AOA é replicação síncrona toouse configurado ou replicação assíncrona. Ao configurar o ouvinte do grupo de disponibilidade do hello, é recomendável que você defina Olá RegisterAllProvidersIP propriedade too0. Isso ocorre porque a conexão do AD do Azure atualmente usa o SQL Native Client tooconnect tooSQL e SQL Native Client não dá suporte para uso de saudação da propriedade MultiSubNetFailover.

## <a name="appendix-csanalyzer"></a>Apêndice: CSAnalyzer
Consulte a seção Olá [verificar](#verify) sobre como toouse esse script.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Próximas etapas
**Tópicos de visão geral**  

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)  
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)  
