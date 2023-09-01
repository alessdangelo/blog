---
title: How I made my own blog
permalink: /posts/how-i-made-my-blog/
layout: single
# author_profile: true
toc: true
toc_sticky: true
excerpt: "I've made my own blog, here's how I did it."
# read_time: true
date: 2023-08-31T13:41:05-04:00
last_modified_at: 2023-09-01T13:57:05-04:00
---

## Introduction

I've had enough time recently to work on something I kept pushing away until now; My blog. As I bought the domain "aless.ch" a few month ago, I've solely used it as a way to share my links, but it wasn't enough, I wanted to be able to share my thoughts on my own platform, this is my train of thought.

Making a blog from scratch would have been an hassle and induce much more headache I would have been prepared for. So I've done some research on what I could use, this is the most relevant and github-pages friendly I found :
    - Jekyll
    - Hugo
    - Gatsby
    - Ghost
Each of them has their strength and weaknesses, but I won't go in details in this article.

I chose Jekyll as it was the most covered online, which helped me on how to setup my project. As Jekyll allows to use a theme as a base, I've tried finding the one that would be modern and not too cluttered, while also being easy to work with.

I've ended up choosing Michael Rose's Minimal Mistakes, which I think is a well made theme. But before that, I tried using Jekyll Garden, which was good but lacking Minimal Mistakes functionality like the side bars, and I didn't have the heart to rework Jekyll Garden completely, so after I bit of tinkering, I switched.

Using Jekyll was not as difficult as I thought it would, especially using Michael Rose's theme, which I could see wanted it to be perfect and that, I like <3.

I won't go in details on how I set the theme up as it has a well made [documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) that explains it better.

I can however, talk about the features I added to it and some settings, such as the theme switcher with a oled toggle, the pac-man themed accent color switcher and the "bits", a collection of quick thoughts and notes; really anything.

## The theme

My palette of choice has been [catppuccin](https://catppuccin-website.vercel.app/) for the last few months so I had to do the same here, so I adjusted the colors accordingly.

### Theme Switch

> courtesy of user [sohamsaha99](https://github.com/sohamsaha99)[on Jan 2, 2021](https://github.com/mmistakes/minimal-mistakes/discussions/2033#discussioncomment-257421)

As this is not a feature supported by Minimal Mistakes, I had to add it manually, using this [thread](https://github.com/mmistakes/minimal-mistakes/discussions/2033) which gave me everything I needed.

Firstly, you got to add a second stylesheet, which will contain the dark theme and be will replace the light theme's stylesheet when switching theme.

> `_config.yml`

```yml
    minimal_mistakes_skin : "catppuccin_latte" 
    minimal_mistakes_skin_dark: "catppuccin_mocha"
```

This added, we need to create a file in our project directory, inside "assets/css" named "theme2.scss" which would contain :

> `assets/css/theme2.scss`

```scss
@charset "utf-8";

@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin2 | default: 'default' }}"; // skin
@import "minimal-mistakes"; // main partials
```

inside "`_includes/head.html`" modify and add the following at the start of the file :

> `_includes/head.html`

``` html
<link rel="stylesheet" href="{{ '/assets/css/main.css' | relative_url }}" id="theme_source">
{% if site.minimal_mistakes_skin_dark %}
<link rel="stylesheet alternate" href="{{ '/assets/css/theme2.css' | relative_url }}" id="theme_source_2">
<script>
let theme = sessionStorage.getItem('theme');
if(theme === "dark")
{
    sessionStorage.setItem('theme', 'dark');
    node1 = document.getElementById('theme_source');
    node2 = document.getElementById('theme_source_2');
    node1.setAttribute('rel', 'stylesheet alternate');
    node2.setAttribute('rel', 'stylesheet');
}
else
{
    sessionStorage.setItem('theme', 'light');
}
</script>
{% endif %}
```

Pairing to a button in the navigation bar, this is the javascript allowing us to change theme.

> `scripts.html`

```html
<script>

function dark_mode_btn_click() {
    var node1 = document.getElementById('theme_source');
    var node2 = document.getElementById('theme_source_2');
    if(node1.getAttribute('rel')=='stylesheet'){
    node2.setAttribute('rel', 'stylesheet');
    setTimeout(function(){
    node1.setAttribute('rel', 'stylesheet alternate');
    }, 5);
    sessionStorage.setItem('theme', 'dark');
}else{
    node1.setAttribute('rel', 'stylesheet');

    setTimeout(function(){
    node2.setAttribute('rel', 'stylesheet alternate');
    }, 5);
    sessionStorage.setItem('theme', 'light');
}
    document.firstElementChild.setAttribute("data-theme", sessionStorage.getItem('theme'));
    changeColor();
    return false;
}

```

And finally, I added a button located in the navigation bar, which allows us to toggle between light & dark.
> `_includes/masthead.html`

```html
{% if site.minimal_mistakes_skin_dark %}

<button class="theme-toggle" id="theme-toggle" title="Toggles light & dark" aria-label="auto" aria-live="polite" type="button" onclick="dark_mode_btn_click();">
<svg class="moonIcon" width="24px" height="24px" stroke-width="1.5" viewBox="0 0 24 24" fill="#ccd7f4" xmlns="http://www.w3.org/2000/svg" color="#ccd7f4">
<path d="M3 11.507a9.493 9.493 0 0018 4.219c-8.507 0-12.726-4.22-12.726-12.726A9.494 9.494 0 003 11.507z" stroke="#ccd7f4" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path>
</svg>

<svg class="sunIcon" width="24px" height="24px" stroke-width="1.5" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
<path d="M12 18a6 6 0 100-12 6 6 0 000 12zM22 12h1M12 2V1M12 23v-1M20 20l-1-1M20 4l-1 1M4 20l1-1M4 4l1 1M1 12h1" opacity="0.5" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"></path>
</svg>
</button>

{% endif %}
```

### Oled toggle

I simply added the following lines inside the footer.html located at `_includes/footer.html` to be able to change the background to pure black when using dark mode :

```html
<div style="position: absolute;left: 0px;right: 0px;display: flex;justify-content: center;align-items: center;">
    <button class="oledButton" type="button" onclick="toggleOled();" title="toggle oled background on dark mode" aria-label="auto" aria-live="polite" style="border-radius: 4px !important; border-color: #1e1e2e;border-style: solid; background-color: black; color: var(--text);font-size: 0.5rem; font-family: 'sans-serif', Quicksand;appearance: none; font-weight: 700;letter-spacing: .1em;">oled!</button>
</div>
```

And these lines inside `_includes/scripts.html`
the function called `toggleOled` will allow us to store the value of the current state of the background and change it accordingly, on the current page.

`reflectOled` on the other hand, will get the current state of the background and reflect it on any page.

```javascript
function toggleOled(){
    if (localStorage.getItem('oled') === 'true') {
        localStorage.setItem('oled', 'false');
        document.documentElement.style.setProperty('--background-color', `#1e1e2e`);
        document.documentElement.style.setProperty('--footer-background-color', `var(--mantle)`);
        return;
    }else{
        localStorage.setItem('oled', 'true');
        document.documentElement.style.setProperty('--background-color', `black`);
        document.documentElement.style.setProperty('--footer-background-color', `black`);
        return;
    }
}

function reflectOled(){
    if (localStorage.getItem('oled') === 'true') {
        document.documentElement.style.setProperty('--background-color', `black`);
        document.documentElement.style.setProperty('--footer-background-color', `black`);
        return;
    }
}
```

And this css code on `_sass/minimal-mistakes/skins/_catppuccin_mocha.scss` will apply our changes

```css
:root{
    --background-color: #1e1e2e;
    --footer-background-color: var(--mantle);
}

footer, .page__footer{
    background-color: var(--footer-background-color) !important;
} 

body, nav, .page__date{
    background-color: var(--background-color) !important;
}
```

We'll hide the oled button on the light theme as it's not needed
> `_sass/minimal-mistakes/skins/_catppuccin_latte.scss`

```css
.oledButton{
    display: none;
}
```

## Wrapping up

As I'm still updating this website, this article will too (I also need to translate it to french). I don't regret going from a pure hand-made static website to a Jekyll powered one as it'll be less of a hassle to maintain. I'm having fun updating and customising my blog to suits my need and reflect my personality, which I'm sure will get more noticeable as I update this blog.
If you're interested in having updates from me, don't forget to check out my links. 
