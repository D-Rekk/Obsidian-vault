> **Title**: Tailwind Tricks
> **Date**: 2023 - 5th Sep
> **Tags**: #CSS #TailwindCSS
---
### Convert PX to REM
To use **rem** instead of **px** in your `tailwind.config` you have to set the font-size to 62.5%. This conversion allows you to use 1/10 px value in rem.
```CSS
@layer base {
	html {
		font-size: 62.5%;
	}
}
```
---
### Define font size and line height

Tailwind allows you to set `font-size` and `line-height` in pairs.
Simply define them as an array of size 2.
___
```JS
theme: {
	fontSize:{
	md: ["1.6rem", "1"],
	lg: ["2.2rem","1rem"],
	"5xl": ["8rem", "120px"],
	}
}

```