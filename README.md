# xss-demo
Demonstrate XSS attack

https://yamamichid.github.io/xss-demo/

## XSS
XSS(Cross-Site Scripting) has three generally recognized forms of XSS:
* Reflected XSS
* Stored XSS
* DOM Based XSS

And they are also categorized to two categories by **where the attack is injected**.
* Server-side XSS
  * Reflected XSS
  * Stored XSS
* Client-side XSS
  * DOM Based XSS

### Relected XSS
```mermaid
sequenceDiagram
    assailant ->> assailant's Server: Put malicious link<br>(http://target-server.com/index.html?search=<script>ajax.send(password)</script>)
    Victim ->> assailant's Server: http://assailant-server.com/index.html
    assailant's Server -->> Victim: index.html
    Victim ->> target Server: http://target-server.com/index.html?search=<script>ajax.send(password)</script>
    target Server ->> target Server: Render response(Attack will be injected here)
    target Server -->> Victim: Rendered response
    Victim ->> Victim: Execute malicious script
    Victim ->> assailant: password
    
```

### Stored XSS
```mermaid
sequenceDiagram
    assailant ->> target Server: Upload malicios data
    Victim ->> target Server: http://target-server.com/index.html
    target Server ->> target Server: Render response(Attack will be injected here)
    target Server -->> Victim: Rendered response
    Victim ->> Victim: Execute malicious script
    Victim ->> assailant: password
    
```

### DOM based XSS
```mermaid
sequenceDiagram
    assailant ->> target Server: Inject some malicious script beforehand somehow(don't care)
    Victim ->> target Server: http://target-server.com/index.html
    target Server -->> Victim: response
    Victim ->> Victim: Render response(Attack will be injected here)
    Victim ->> Victim: Execute malicious script
    Victim ->> assailant: password
    
```

## References
* https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html#:~:text=The%20primary%20difference%20is%20where%20the%20attack%20is,XSS%20is%20a%20client%20%28browser%29%20side%20injection%20issue.
