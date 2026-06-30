- In the **Payloads** tab of Burp Suite Intruder, we can create, assign, and configure payloads for an attack. This sub-tab is divided into four sections:
![[Pasted image 20260527112834.png]]

### Payload Sets

This section lets us choose the position where the payload will be inserted and select the payload type to use.

- In attack types that use only one payload set, such as **Sniper** or **Battering Ram**, the **Payload Set** dropdown will contain only one option, no matter how many positions are selected.
- In attack types that use multiple payload sets, such as **Pitchfork** or **Cluster Bomb**, there will be one dropdown item for each position.

**Note:**  
When multiple positions are used, payload set numbering follows a **top-to-bottom, left-to-right** order.  
Example:

```
username=§pentester§&password=§Expl01ted§
```

- Payload Set 1 → username field
- Payload Set 2 → password field

### Payload Settings

This section contains options related to the selected payload type.

For example, with the **Simple list** payload type, we can:

- manually add payloads
- paste multiple lines
- load payloads from a file

Other options include:

- **Remove** → deletes the selected payload
- **Clear** → removes all payloads from the list

Be careful when loading very large lists, as they may cause Burp Suite to crash.

Each payload type has its own settings and features, so exploring them helps understand different attack possibilities.

### Payload Processing

This section allows us to apply rules to payloads before they are sent to the target.

Examples:

- capitalize words
- skip payloads matching a regex
- modify or filter payloads

Although not always needed, this section is useful when special payload formatting or filtering is required.

### Payload Encoding

This section controls how payloads are encoded.

By default, Burp Suite URL-encodes payloads to ensure safe transmission. However, we can customize this behavior by:

- changing which characters are encoded
- disabling the **“URL-encode these characters”** option

These settings give us greater control over how payloads are sent during testing and exploitation.

# Next Topic : [[Introduction to Attacks types]]