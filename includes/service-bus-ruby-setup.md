## <a name="create-a-ruby-application"></a><span data-ttu-id="4c4ce-101">Criar um aplicativo Ruby</span><span class="sxs-lookup"><span data-stu-id="4c4ce-101">Create a Ruby application</span></span>
<span data-ttu-id="4c4ce-102">Para obter instruções, confira [Criar um aplicativo Ruby no Azure (a página pode estar em inglês)](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="4c4ce-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="4c4ce-103">Configurar seu tooUse barramento de serviço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4c4ce-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="4c4ce-104">toouse barramento de serviço, baixe e use o pacote do Azure Ruby hello, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="4c4ce-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="4c4ce-105">Use o pacote de saudação do RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="4c4ce-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="4c4ce-106">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="4c4ce-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="4c4ce-107">Digite "gem instalar o azure" em gem de Olá Olá comando janela tooinstall e dependências.</span><span class="sxs-lookup"><span data-stu-id="4c4ce-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="4c4ce-108">Importar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="4c4ce-108">Import hello package</span></span>
<span data-ttu-id="4c4ce-109">Usando seu editor de texto favorito, adicione Olá toohello superior de saudação Ruby a seguir na qual você pretende toouse armazenamento de arquivo:</span><span class="sxs-lookup"><span data-stu-id="4c4ce-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="4c4ce-110">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="4c4ce-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="4c4ce-111">Tooset valores de saudação do namespace, nome da saudação de código a seguir de saudação do uso chave, chave, o signatário e host:</span><span class="sxs-lookup"><span data-stu-id="4c4ce-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="4c4ce-112">Definir Olá namespace toohello valor criado em vez de URL inteira hello.</span><span class="sxs-lookup"><span data-stu-id="4c4ce-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="4c4ce-113">Por exemplo, use **"yourexamplenamespace"**, não "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="4c4ce-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
