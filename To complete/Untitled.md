> **Title**: Untitled
> **Date**: 2023/ 4th Aug
> **Tags**: 
---
```JS
function initialLoad(){

for (let i = 2; i <= 4; i++) {

const parent = document.querySelector(`#sections > ytd-guide-section-renderer:nth-child(${i}) > h3`)

let isCompact = localStorage.getItem(`ImprovedTube-compact-${i}`) === "true"

isCompact ? appendStyle(i) : (styles[i-2] = null)

parent.addEventListener("click", () => {toggleStyle(i)})

}

}

function toggleStyle(index) {

if (styles[index] && styles[index].parentNode) { //removing

document.head.removeChild(styles[index]);

styles[index] = null;

} else appendStyle(index);

localStorage.setItem(`ImprovedTube-compact-${index}`, !!styles[index])

}

function appendStyle(index){

const cssRules = `

#sections > ytd-guide-section-renderer:nth-child(${index}) > #items{

display:none;

};`

const style = document.createElement("style");

style.appendChild(document.createTextNode(cssRules));

styles[index] = style

document.head.appendChild(styles[index])

console.log("We appended this style:");

console.log(styles[index]);

}
```