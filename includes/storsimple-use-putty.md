<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="3e4e3-101">tooconnect por meio do console serial Olá</span><span class="sxs-lookup"><span data-stu-id="3e4e3-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="3e4e3-102">Conecte o dispositivo de toohello de cabo serial (diretamente ou através de um adaptador serial USB).</span><span class="sxs-lookup"><span data-stu-id="3e4e3-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="3e4e3-103">Olá abrir **painel de controle**e, em seguida, abra Olá **Gerenciador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="3e4e3-104">Identifique a porta de saudação COM conforme mostrado na ilustração a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Conectando por meio do console serial](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="3e4e3-106">Inicie o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="3e4e3-107">No painel direito da saudação, alterar Olá **o tipo de Conexão** muito**Serial**.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="3e4e3-108">No painel direito da saudação, digite a porta COM apropriada de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="3e4e3-109">Certifique-se de que os parâmetros de configuração serial Olá são definidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3e4e3-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="3e4e3-110">Velocidade: 115.200</span><span class="sxs-lookup"><span data-stu-id="3e4e3-110">Speed: 115,200</span></span>
   * <span data-ttu-id="3e4e3-111">Bits de dados: 8</span><span class="sxs-lookup"><span data-stu-id="3e4e3-111">Data bits: 8</span></span>
   * <span data-ttu-id="3e4e3-112">Bits de parada: 1</span><span class="sxs-lookup"><span data-stu-id="3e4e3-112">Stop bits: 1</span></span>
   * <span data-ttu-id="3e4e3-113">Paridade: nenhuma</span><span class="sxs-lookup"><span data-stu-id="3e4e3-113">Parity: None</span></span>
   * <span data-ttu-id="3e4e3-114">Controle de fluxo: nenhum</span><span class="sxs-lookup"><span data-stu-id="3e4e3-114">Flow control: None</span></span>
     
     <span data-ttu-id="3e4e3-115">Essas configurações são mostradas na ilustração a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-115">These settings are shown in hello following illustration.</span></span>
     
     ![Configurações do PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="3e4e3-117">Se saudação padrão controle de fluxo não funcionar, tente configurar o controle de fluxo da saudação tooXON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="3e4e3-118">Clique em **abrir** toostart uma sessão serial.</span><span class="sxs-lookup"><span data-stu-id="3e4e3-118">Click **Open** toostart a serial session.</span></span>

