<!--author=SharS last changed: 12/01/15-->

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="205b3-101">Para entrar no modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="205b3-101">To enter Maintenance mode</span></span>
1. <span data-ttu-id="205b3-102">No menu do console serial, escolha a opção 1, **Efetuar login com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="205b3-102">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
2. <span data-ttu-id="205b3-103">Digite a senha.</span><span class="sxs-lookup"><span data-stu-id="205b3-103">Type the password.</span></span> <span data-ttu-id="205b3-104">A senha padrão é **Senha1**.</span><span class="sxs-lookup"><span data-stu-id="205b3-104">The default password is **Password1**.</span></span>
3. <span data-ttu-id="205b3-105">No prompt de comando, digite</span><span class="sxs-lookup"><span data-stu-id="205b3-105">At the command prompt, type</span></span>
   
     `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="205b3-106">Você verá uma mensagem de aviso informando que o modo de Manutenção interromperá todas as solicitações de E/S e a conexão com o portal clássico do Azure, e você será solicitado a confirmar.</span><span class="sxs-lookup"><span data-stu-id="205b3-106">You will see a warning message telling you that Maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="205b3-107">Digite **Y** para entrar no modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="205b3-107">Type **Y** to enter Maintenance mode.</span></span>
   
    <span data-ttu-id="205b3-108">Ambos os controladores serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="205b3-108">Both controllers will restart.</span></span> <span data-ttu-id="205b3-109">Quando a reinicialização estiver concluída, outra mensagem será exibida indicando que o dispositivo está em modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="205b3-109">When the restart is complete, another message will appear indicating that the device is in Maintenance mode.</span></span>

