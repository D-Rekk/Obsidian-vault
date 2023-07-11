- [ ] Help someone
- [ ] Say what to do
> I should move the **chapters** to the sidebar 

```JS
let element = document.querySelector('ytd-engagement-panel-section-list-renderer[target-id="engagement-panel-macro-markers-description-chapters"]');

document.querySelector("#secondary-inner #playlist").insertAdjacentElement("beforebegin", element)
```
-
