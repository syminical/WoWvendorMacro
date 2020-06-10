# WoW 3.3.5 Vendor Recipe Macro

This macro can quickly purchase **[Formula: Runed Arcanite Rod]** from Lorelae Wintersong in Moonglade. It can be customized to work with any vendor and any items they sell.
This is useful for fresh servers. There will be a lot of players trying to buy it, and this macro will give you a fighting chance; unless your ping has it out for you.

### Setup
1. In-game press **ESC** to bring up the menu, then click on the **Macros** button.
2. Create a new macro, enter a name, pick an icon. ( A single space looks best, imo. )
3. Copy the code from the **vendorMacro.lua** link above, and paste it into the text box ingame.
4. Drag the macro icon to your hotkey bar. ( Remember this slot! )
5. Bring up the **ESC** menu again, and click **Key Bindings**.
6. Bind the slot you dropped the macro icon on to your mouse's scroll wheel. (  up or down )
7. Scroll down to **Targeting Fuctions**, and bind **Interact With Target** to the other direction of the mouse wheel.
8. Consider making a separate macro to quickly target the npc, just in case.
   * `/target Lorelae Wintersong`

### Use
1. Have the NPC targeted.
2. Scroll the mouse wheel in the direction that you bound to open the shop.
3. Scroll in the other direction.
4. Repeat. **FAST**.  
**BTW...** you can tell it is working if you see the shop opening and closing. The interact bind opens the shop, and the macro closes it after trying to buy the item.

### Advice
* Your ping **(lag)** will play a large part in beating other players who may also be using a macro.
  - You may miss the item, but maybe you can at least get the spawn timer from the time stamp. Try again later?
* This is not optimal mouse wheel spam! You need to spam **BOTH** directions quickly!!
  * Try out long and short swipes; the goal is to spam the sweet spot between scrolling up and then scrolling down. Scrolling up or down too long is bad.
* This particular recipe respawned every 15 min on my server, and the npc's death did not restart the item's respawn timer.
* The vendor sells it for **2g 20s**, so come prepared.
* Use the time stamp from the macro to figure out the item's respawn time. It can change upon server restart, or from slow buys.  
  ![Success time stamp example.](images/successfulPurchase.png)  
  **Above**: The macro saw the item, bought it, saw it again before the shop updated, all in under a second.  
  **[Formula: Runed Arcanite Rod]**'s respawn timer creates a 1 hour cycle. Add **15min** to the time stamp until it is complete.  Start spamming maybe a minute early until you see it.
  **> ... 11:39, 11:54, 12:09, 12:24 , 12:39, ...** 

### Customize
* Buy a different Item:
  1. Find out the slot number the item has in the shop inventory. It can change if there are other limited quantity recipes with a lower slot number than your target item.  
     Use the macro from the **listItemsMacro.lua** link above with a shop open to get the output below:  
     ![Slot id macro example.](images/itemIDScan.png)  
     Notice how the number for **[Formula: Runed Arcanite Rod]** is **30**? There is another **Formula** above it **(29)**, which may be sold out when our target item spawns.
     For this npc, there are no other limited quantity items above our target that can change its slot; therefore the only slots our target will be in are **29** and **30**.  
     **NOTE** It may be difficult to get such an accurate print out on a high population server.
  2. Now that you know the slot number, change the `for` loop values in the script to scan only the slots you need. The more slots scanned, the slower the script.  
     `for i=START,STOP`  ( **START** & **STOP** are index integers )
  3. Edit the `if` statement to match just enough characters to confirm your purchase. For **[Formula: Runed Arcanite Rod]**, it is not enough to search for part of **Formula** since there is another formula. It is not reasonable to expect to buy both and beat other macros unless you have much lower ping than your competition. ( Just one is hard. )  
     **NOTE** WoW's `/script` uses the **LUA** language; LUA starts counting with **1** not **0**, unlike some other programming languages.
  4. Take a look at the [**WoW API**](https://wowwiki.fandom.com/wiki/World_of_Warcraft_API) for more information on specific functions that are available.

### How Does It Work?
* The macro is fast because it searches specific spots and slots, in item names and shops, instead of scanning the full info of every item the vendor has.
* The macro verifies small parts of the item's info string to confirm purchases.
* **In a nutshell**:
  1. The script uses a `for` loop to search a predefined number of **specific** slots in the shop inventory.
     - `GetMerchantItemInfo(i)` contains the item's name, and some other info, but the name is at the start of the string. Index **1** is the first character, starting from the left, and each character has its own index.
  2. The name is tested to confirm it is the correct item. This does slow things down, but it is necessary so that the macro can be spammed without wasting your gold.
     - Some items may require multiple if statements to check different spots of the name. This depends on how unique the item's name is in the shop inventory.  
       For **[Formula: Runed Arcanite Rod]** checking **index 10** for the character `'R'` is safe enough. If you choose to use multiple tests, save the result of `GetMerchantItemInfo(i)` to a variable so that you do not waste time re-requesting it.
  3. At this point the name test either **fails** or **succeeds**:
     - **SUCCESS**  
       The item is purchased, a time stamp is sent to your chat, and the loop is broken.
     - **FAIL**  
       Move on to the next slot if there are any left to check.
  4. The shop window is closed so that you can reopen it with the keybind to refresh and retry. This also provides some feedback while spamming.
  
  Good luck! ;)