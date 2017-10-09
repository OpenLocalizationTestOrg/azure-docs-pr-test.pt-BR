---
title: aplicativo de exemplo aaaAzure para uso com DMZs | Microsoft Docs
description: "Implantar esse aplicativo da web simples depois de criar uma rede de Perímetro tootest cenários de fluxo de tráfego"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a>Aplicativo de exemplo para uso com DMZs
[Retornar toohello página segurança limite de melhores práticas][HOME]

Esses scripts do PowerShell podem ser executados localmente em Olá IIS01 e AppVM01 tooinstall de servidores e configurar um aplicativo web simples que exibe uma página html do servidor front-end de IIS01 Olá com conteúdo do servidor de AppVM01 Olá back-end.

Esse aplicativo fornece um ambiente de teste simples para muitos dos exemplos de DMZ hello e como as alterações no hello pontos de extremidade, NSGs, UDR e regras de Firewall podem afetar os fluxos de tráfego.

## <a name="firewall-rule-tooallow-icmp"></a>Tooallow de regra de firewall ICMP
Essa instrução simple do PowerShell pode ser executada em qualquer tráfego ICMP (Ping) tooallow VM do Windows. Permite que essa atualização de firewall para facilitar o teste e solução de problemas, permitindo que Olá ping protocolo toopass através do firewall do windows hello (para a maioria das distribuições de Linux que ICMP é ativado por padrão).

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

Se você usar Olá scripts a seguir, essa adição de regra de firewall é a primeira instrução de saudação.

## <a name="iis01---web-application-installation-script"></a>IIS01 — Script de instalação do aplicativo Web
Este script:

1. Abra IMCPv4 (Ping) no firewall do windows hello servidor local para o teste mais fácil
2. Instalar o IIS e Olá .net v Framework 4.5
3. Criará uma página da Web ASP.NET e um arquivo de Web.config
4. Alterar o saudação padrão aplicativo pool toomake arquivo acesso mais fácil
5. Conta de administrador do conjunto Olá usuário anônimo tooyour e a senha

Esse script do PowerShell deve ser executado localmente com RDP em IIS01.

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a>AppVM01 — Script de instalação do servidor de arquivos
Esse script configura Olá back-end para este aplicativo simple. Este script:

1. Abra IMCPv4 (Ping) no firewall Olá para teste mais fácil
2. Crie um diretório para o site da web de saudação
3. Criar um toobe do arquivo de texto remotamente acessar pela página de web Olá
4. Definir permissões em tooAnonymous de arquivo e diretório Olá tooallow acesso
5. Desativar tooallow de segurança reforçada do IE mais fácil de pesquisa deste servidor 

> [!IMPORTANT]
> **Prática recomendada**: nunca desativar segurança reforçada do Internet Explorer em um servidor de produção, além de geralmente é uma web de saudação toosurf boa ideia de um servidor de produção. Além disso, abrir compartilhamentos de arquivos para acesso anônimo é uma ideia ruim, mas que foi executado aqui para simplificar.
> 
> 

Esse script do PowerShell deve ser executado localmente com RDP em AppVM01. O PowerShell é necessário toobe executar como a execução bem-sucedida do administrador tooensure.

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a>DNS01 — Script de instalação do servidor DNS
Não há nenhum script incluído no tooset de aplicativo neste exemplo o servidor DNS hello. Se o teste de regras de firewall hello, NSG ou UDR precisa tooinclude o tráfego de DNS, o servidor de saudação DNS01 precisa toobe configurar manualmente. arquivo de xml de configuração de rede de saudação e modelo do Gerenciador de recursos para ambos os exemplos incluem DNS01 como servidor DNS primário do hello e servidor DNS público Olá hospedado pelo nível 3 como servidor de DNS backup Olá. servidor de nível 3 DNS Olá seria Olá real DNS do servidor usado para tráfego não local e com DNS01 sem configurar, nenhuma rede local DNS ocorreria.

## <a name="next-steps"></a>Próximas etapas
* Execute o script de IIS01 de saudação em um servidor IIS
* Executar um script de Servidor de Arquivos em AppVM01
* Procurar toohello IP público em IIS01 toovalidate sua compilação

<!--Link References-->
[HOME]: ../best-practices-network-security.md
