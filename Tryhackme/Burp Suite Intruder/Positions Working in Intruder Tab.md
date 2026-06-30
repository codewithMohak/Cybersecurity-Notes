- When using Burp Suite Intruder for an attack, the first step is to identify the positions in the request where payloads should be inserted. These positions tell Intruder where the payloads will be placed during the attack.
- Now, let’s move to the **Positions** tab:![[Pasted image 20260527112033.png]]
- Burp Suite automatically tries to detect the most likely positions where payloads can be inserted. These positions are highlighted in green and marked with section symbols (§).

On the right side of the interface, there are three buttons: **Add §**, **Clear §**, and **Auto §**.

- **Add §:** Lets us manually define new positions by selecting part of the request and clicking the button.
- **Clear §:** Removes all selected positions, giving us a blank request where we can define our own positions.
- **Auto §:** Automatically detects the most likely positions in the request. This is useful if we cleared the default positions and want to restore them.

## Next Topic : [[Payloads Working in Intruder Tab]]