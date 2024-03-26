## About

Simple application for login in **SvelteKit** with error handling.

### Comments on Impementation and Testing

There are certainly different ways to approach the error handling here. Mine chosen solution is perhaps a bit more verbose, but should safely handle all error states, while at the same time getting specified data even from requests returning 4xx status, which made me give it priority in the end.

Apart from the four mentioned **response "types"**, I found also state, when user doesn't enter any credentials in User Code, which returns mentioned "messages" data only in an errors object with: ["User Code cannot be blank."]. Login was tested via given VPN and also a **proxy** (proxy was created because of a CORS issue), which remains in the code. **Please just replace url in fetch with your given original url, which is commented out between my localhost with a proxy**. SvelteKit app was created with also typescript rules, but in the end verbose ts definitions were not used for the purposes of this app. Code was formatted with **Prettier** support for Svelte. For futher features, further endpoints would need to be supplied.
