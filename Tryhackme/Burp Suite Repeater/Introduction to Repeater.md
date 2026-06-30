# **What is Repeater?**
- **Burp Suite Repeater enables us to modify and resends the intercept requests to the target designation. 
- **It allows us to take requests captured in the Burp Suite and manipulate them, sending them repeatedly as needed**.![[Pasted image 20260526171548.png]]
### **Request Line** : 
- Located at the top of the left  the tab, it display the list of Repeater requests.
### **Request Controls** : 
- It is directly below to the **request line** , these control allow us to send a requests, cancel and hanging the requests.
### **Request and Response View** :
- We can edit the requests in the Requests view and then forwarding , while the corresponding response will shown in the Response view.
### **Layout Options** :
- Located at the top-right of the Request/Response view, these options enable us to customize the layout of the Request and Response views.
### **Inspector** :
- Located on the right side, the Inspector helps us analyze and edit requests more easily than the raw editor.
### **Target** :
- Located above the Inspector, the Target field shows the IP address or domain where the requests are sent.

## **Basic Usage**

### Utilization of Keyboard Shortcut : `Ctrl+R`.

- If we want to change any part of the request, we can simply edit it in the Request view and click **Send** again. The Response view on the right will then update automatically.
- For example, if we change the `Connection` header value from `"close"` to `"open"`, the response will contain a `Connection` header with the value `"keep-alive"`.![[Pasted image 20260526211718.png]]


### Next Topic : [[]]