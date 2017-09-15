## <a name="create-a-ruby-application"></a><span data-ttu-id="db8ef-101">Criar um aplicativo Ruby</span><span class="sxs-lookup"><span data-stu-id="db8ef-101">Create a Ruby application</span></span>
<span data-ttu-id="db8ef-102">Para obter instruções, confira [Criar um aplicativo Ruby no Azure (a página pode estar em inglês)](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="db8ef-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="db8ef-103">Configurar seu aplicativo para usar o Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="db8ef-103">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="db8ef-104">Para usar o Barramento de Serviço, baixe e use o pacote do Azure Ruby, que inclui um conjunto de bibliotecas convenientes que se comunicam com os serviços REST de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="db8ef-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="db8ef-105">Usar RubyGems para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="db8ef-105">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="db8ef-106">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="db8ef-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="db8ef-107">Digite "gem install azure" na janela de comandos para instalar a gema e as dependências.</span><span class="sxs-lookup"><span data-stu-id="db8ef-107">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="db8ef-108">Importar o pacote</span><span class="sxs-lookup"><span data-stu-id="db8ef-108">Import the package</span></span>
<span data-ttu-id="db8ef-109">Usando seu editor de texto favorito, adicione o seguinte na parte superior do arquivo do Ruby no qual você pretende usar o armazenamento:</span><span class="sxs-lookup"><span data-stu-id="db8ef-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="db8ef-110">Configurar uma conexão do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="db8ef-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="db8ef-111">Use o código a seguir para definir os valores de namespace, nome da chave, chave, assinante e host:</span><span class="sxs-lookup"><span data-stu-id="db8ef-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="db8ef-112">Defina o valor do namespace para o valor que você criou, em vez de toda a URL.</span><span class="sxs-lookup"><span data-stu-id="db8ef-112">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="db8ef-113">Por exemplo, use **"yourexamplenamespace"**, não "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="db8ef-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
