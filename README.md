# WoW 3.3.5 Vendor Recipe Macro

This macro can quickly purchase **[Formula: Runed Arcanite Rod]** from Lorelae Wintersong in Moonglade. It can be customized to work with any vendor and any items they sell.
This is useful for fresh servers. There will be a lot of players trying to buy it, and this macro will give you a fighting chance; unless your ping has it out for you.

### Setup
1. In-game press esc to bring up the menu, then click on the **Macros** button.
2. Create a new macro, enter a name, pick an icon. ( A single space looks best, imo. )
3. Paste the code into the text box.
4. Drag the macro icon to your hotkey bar. ( Remember this slot! )
5. Press esc again, and click **Key Bindings**.
6. Bind the slot holding the macro to your mouse's scroll wheel.
7. Scroll down to **Targeting Fuctions**, and bind **Interact With Target** to the other direction of the mouse wheel.
8. Consider making a separate macro to target the npc, just in case.
  * 
  ```
  /target Lorelae Wintersong
  ```

### Use
1. Have the NPC targeted.
2. Scroll the mouse wheel in the direction that you bound to open the shop.
3. Scroll in the other direciton.
4. Repeat.  
**BTW...** you can tell it is working if you see the shop opening and closing. The interact bind opens the shop, and the macro closes it after trying to buy the item.

### Advice
* Your ping **(lag)** will play a large part in beating other players who may also be using a macro.
* This is not optimal mouse wheel spam! You need to spam **BOTH** directions quickly!!
  * Try out long and short swipes; the goal is to spam the sweet spot between scrolling up and then scrolling down. Scrolling up or down too long is bad.
* This particular recipe respawned every 15 min on my server, and the npc's death did not restart the item's respawn timer.
* The vendor sells it for 2g20s, so come prepared.

### Customize

### How Does It Work?
* The macro is fast because it searches specific spots instead of scanning every item the vendor has.
  * To find the spot: /script for i=1,GetMerchantNumItems() do print(i, GetMerchantItemInfo(i)) end