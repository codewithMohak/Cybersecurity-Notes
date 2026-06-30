Intruder is Burp Suite’s built-in fuzzing tool used for automated request modification and repeated testing with different input values. Using a captured request, usually from the Proxy module, Intruder can send multiple requests with modified values based on user-defined settings.

It can be used for tasks such as:

- brute-forcing login forms using username and password wordlists
- fuzzing subdirectories, endpoints, or virtual hosts with wordlists

Intruder works similarly to command-line tools like Wfuzz or ffuf.

However, in Burp Community Edition, Intruder is rate-limited, making it much slower than the Professional version. Because of this, many security professionals prefer other tools for fuzzing and brute-forcing. Even so, Intruder is still a useful tool and worth learning.

Let’s now explore the Intruder interface:
![[Pasted image 20260527103612.png]]

The initial Intruder interface is simple and allows us to choose a target. If a request is sent from the Proxy using **Ctrl + I** or by right-clicking and selecting **“Send to Intruder”**, the target field is filled automatically.

Intruder contains four sub-tabs:

- **Positions:** Used to choose the attack type and define where payloads will be inserted in the request template.
- **Payloads:** Used to select the values that will be inserted into the positions defined earlier. Payloads can be loaded from sources like wordlists. This tab also allows modifying payload behavior, such as adding prefixes or suffixes, performing match and replace, or skipping payloads using regex rules.
- **Resource Pool:** Mainly useful in Burp Professional for managing resources between automated tasks. In Burp Community Edition, this tab has limited use.
- **Settings:** Used to configure attack behavior, such as handling results, marking requests with specific text, or controlling how Burp responds to redirect (3xx) responses.

**Note:**  
Fuzzing is the process of testing functionality or checking for resources by sending different input values to a parameter. For example, endpoint fuzzing appends words from a wordlist to a URL like:

```
http://10.48.156.101/WORD_GOES_HERE
```

The server’s response is then analyzed to identify valid endpoints or functionality.

## Next Topic : [[Positions Working in Intruder Tab]]