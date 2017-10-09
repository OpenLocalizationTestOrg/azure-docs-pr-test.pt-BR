## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="64fb8-101">Preparar o Intel NUC</span><span class="sxs-lookup"><span data-stu-id="64fb8-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="64fb8-102">configuração de hardware do toocomplete hello, você precisa:</span><span class="sxs-lookup"><span data-stu-id="64fb8-102">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="64fb8-103">Conecte-se a fonte de alimentação Intel NUC toohello incluída no kit de saudação.</span><span class="sxs-lookup"><span data-stu-id="64fb8-103">Connect your Intel NUC toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="64fb8-104">Conecte-se a rede de tooyour Intel NUC usando um cabo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="64fb8-104">Connect your Intel NUC tooyour network using an Ethernet cable.</span></span>

<span data-ttu-id="64fb8-105">Você acabou de concluir instalação de hardware de saudação do seu dispositivo de gateway NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="64fb8-105">You have now completed hello hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="64fb8-106">Entrar e acessar terminal Olá</span><span class="sxs-lookup"><span data-stu-id="64fb8-106">Sign in and access hello terminal</span></span>

<span data-ttu-id="64fb8-107">Você tem um ambiente de terminal tooaccess de duas opções no seu NUC Intel:</span><span class="sxs-lookup"><span data-stu-id="64fb8-107">You have two options tooaccess a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="64fb8-108">Se você tiver um teclado e monitorar conectado tooyour NUC Intel, você pode acessar diretamente o shell hello.</span><span class="sxs-lookup"><span data-stu-id="64fb8-108">If you have a keyboard and monitor connected tooyour Intel NUC, you can access hello shell directly.</span></span> <span data-ttu-id="64fb8-109">as credenciais padrão Olá são username **raiz** e a senha **raiz**.</span><span class="sxs-lookup"><span data-stu-id="64fb8-109">hello default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="64fb8-110">Shell de saudação de acesso no seu NUC Intel usando SSH em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="64fb8-110">Access hello shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="64fb8-111">Entre com o SSH</span><span class="sxs-lookup"><span data-stu-id="64fb8-111">Sign in with SSH</span></span>

<span data-ttu-id="64fb8-112">toosign com SSH, é necessário o endereço IP de saudação do seu NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="64fb8-112">toosign in with SSH, you need hello IP address of your Intel NUC.</span></span> <span data-ttu-id="64fb8-113">Se você tiver um teclado e monitorar conectado tooyour NUC Intel, use Olá `ifconfig` toofind endereço IP de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="64fb8-113">If you have a keyboard and monitor connected tooyour Intel NUC, use hello `ifconfig` command toofind hello IP address.</span></span> <span data-ttu-id="64fb8-114">Como alternativa, conecte-se a endereços de saudação do tooyour roteador toolist de dispositivos na sua rede.</span><span class="sxs-lookup"><span data-stu-id="64fb8-114">Alternatively, connect tooyour router toolist hello addresses of devices on your network.</span></span>

<span data-ttu-id="64fb8-115">Entre com o nome de usuário **raiz** e a senha **raiz**.</span><span class="sxs-lookup"><span data-stu-id="64fb8-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="64fb8-116">Opcional: Compartilhar uma pasta em seu Intel NUC</span><span class="sxs-lookup"><span data-stu-id="64fb8-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="64fb8-117">Opcionalmente, talvez você queira tooshare uma pasta no seu NUC Intel com seu ambiente de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="64fb8-117">Optionally, you may want tooshare a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="64fb8-118">Uma pasta de compartilhamento permite que você toouse seu editor de texto preferido de área de trabalho (como [código do Visual Studio](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit arquivos em seu NUC Intel, em vez de usar `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="64fb8-118">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="64fb8-119">tooshare uma pasta com o Windows, configure um servidor do Samba no hello NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="64fb8-119">tooshare a folder with Windows, configure a Samba server on hello Intel NUC.</span></span> <span data-ttu-id="64fb8-120">Como alternativa, use servidor SFTP Olá em Olá Intel NUC com um cliente SFTP em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="64fb8-120">Alternatively, use hello SFTP server on hello Intel NUC with an SFTP client on your desktop machine.</span></span>
