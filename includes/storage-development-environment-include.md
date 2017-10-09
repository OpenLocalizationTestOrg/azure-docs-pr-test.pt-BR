## <a name="set-up-your-development-environment"></a>Configurar seu ambiente de desenvolvimento
Em seguida, configure seu ambiente de desenvolvimento no Visual Studio para que você está pronto tootry Olá exemplos de código neste guia.

### <a name="create-a-windows-console-application-project"></a>Criar um projeto de aplicativo de console do Windows.
No Visual Studio, crie um novo aplicativo de console do Windows. Olá, as etapas a seguir mostra como toocreate um aplicativo de console no Visual Studio de 2017, no entanto, etapas de saudação são semelhantes em outras versões do Visual Studio.

1. Selecione **Arquivo** > **Novo** > **Projeto**
2. Selecione **Instalado** > **Modelos** > **Visual C#** > **Área de trabalho clássica do Windows**
3. Selecione **Aplicativo do Console (.NET Framework)**
4. Insira um nome para seu aplicativo no hello **nome:** campo
5. Selecione **OK**

![Diálogo de criação de projeto no Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Todos os exemplos de código neste tutorial podem ser adicionados toohello `Main()` método do seu aplicativo de console `Program.cs` arquivo.

Você pode usar o hello biblioteca de cliente de armazenamento do Azure em qualquer tipo de aplicativo .NET, incluindo um aplicativo de web ou serviço de nuvem do Azure e aplicativos de desktop e mobile. Neste guia, usamos um aplicativo de console para simplificar.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Usar os pacotes do NuGet tooinstall Olá necessária
Existem dois pacotes, você precisa tooreference em seu projeto toocomplete este tutorial:

* [Biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): Este pacote fornece acesso programático a recursos toodata na sua conta de armazenamento.
* [Biblioteca do Gerenciador de Configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este pacote fornece uma classe para analisar uma cadeia de conexão em um arquivo de configuração, independentemente de onde o aplicativo está sendo executado.

Você pode usar ambos os pacotes do NuGet tooobtain. Siga estas etapas:

1. Clique com o botão direito do mouse no seu projeto no **Gerenciador de Soluções** e escolha **Gerenciar Pacotes NuGet**.
2. Pesquisar online "Windowsazure" e clique em **instalar** tooinstall Olá biblioteca de cliente de armazenamento e suas dependências.
3. Pesquisar online "WindowsAzure.ConfigurationManager" e clique em **instalar** tooinstall hello Azure Configuration Manager.

> [!NOTE]
> pacote de biblioteca de cliente de armazenamento Olá também está incluído no hello [SDK do Azure para .NET](https://azure.microsoft.com/downloads/). No entanto, é recomendável que você também instale Olá biblioteca de cliente de armazenamento do NuGet tooensure que você sempre tenha a versão mais recente Olá Olá da biblioteca de cliente.
> 
> dependências de ODataLib Olá Olá biblioteca de cliente de armazenamento para .NET são resolvidas por pacotes de ODataLib Olá disponíveis no NuGet, não do WCF Data Services. bibliotecas de ODataLib Olá podem ser baixadas diretamente ou referenciadas pelo seu projeto de código através do NuGet. pacotes ODataLib específicos Olá usados pelo Olá biblioteca de cliente de armazenamento são [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), e [espacial](http://nuget.org/packages/System.Spatial/). Embora essas bibliotecas são usadas pelas classes de armazenamento de tabela do Azure hello, eles são dependências necessárias para a programação com hello biblioteca de cliente de armazenamento.
> 
> 

### <a name="determine-your-target-environment"></a>Determinar o ambiente de destino
Você tem duas opções de ambiente para executar os exemplos de saudação neste guia:

* Você pode executar seu código em uma conta de armazenamento do Azure na nuvem hello. 
* Você pode executar o código no emulador de armazenamento do Azure hello. emulador de armazenamento Olá é um ambiente local que emula uma conta de armazenamento do Azure na nuvem hello. emulador de saudação é uma opção gratuita para testar e depurar seu código enquanto seu aplicativo está em desenvolvimento. emulador de saudação usa uma conta bem conhecida e a chave. Para obter mais informações, consulte [Olá Use Azure Storage Emulator para desenvolvimento e teste](../articles/storage/common/storage-use-emulator.md)

Se você tiver como alvo uma conta de armazenamento em nuvem Olá, copie a chave de acesso primária de Olá para sua conta de armazenamento da saudação portal do Azure. Para saber mais, confira [Exibir e copiar chaves de acesso de armazenamento](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).

> [!NOTE]
> Você pode direcionar tooavoid de emulador de armazenamento Olá incorrer em todos os custos associados com o armazenamento do Azure. No entanto, se você escolher tootarget uma conta de armazenamento do Azure na nuvem hello, custos para executar este tutorial será insignificante.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Configurar a cadeia de conexão de armazenamento
Olá biblioteca de cliente de armazenamento do Azure para .NET oferece suporte ao uso de um pontos de extremidade de tooconfigure de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de armazenamento. Olá melhor maneira toomaintain sua cadeia de caracteres de conexão de armazenamento está em um arquivo de configuração. 

Para obter mais informações sobre cadeias de caracteres de conexão, consulte [configurar tooAzure uma cadeia de caracteres de Conexão armazenamento](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> Sua chave de conta de armazenamento é a senha da sua conta de armazenamento raiz de toohello semelhante. Sempre ser tooprotect cuidado sua chave de conta de armazenamento. Evitar a distribuição de usuários tooother, codificar, ou salvá-lo em um arquivo de texto sem formatação que é acessível tooothers. Regenerar a chave usando Olá portal do Azure se você acredita que ele pode ter sido comprometido.
> 
> 

tooconfigure sua cadeia de caracteres de conexão, abra Olá `app.config` arquivo no Gerenciador de soluções no Visual Studio. Adicionar conteúdo Olá Olá `<appSettings>` elemento mostrado abaixo. Substituir `account-name` com o nome de saudação da sua conta de armazenamento e `account-key` com sua chave de acesso da conta:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Por exemplo, a configuração é semelhante a:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

emulador de armazenamento do tootarget hello, você pode usar um atalho que mapeia a chave e o nome de conta conhecida do toohello. Nesse caso, a configuração da cadeia de conexão é:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

