---
tags:
  - wordpress
  - oxygen builder
  - design
  - blog
  - redesign
  - prototype
---

# Lighthouse Labs

## Design decisions

1. Subscription section
- New header
    - Subscription CTA
    - Light/dark
2. Full page menu
3. Mouse follow animation header section
4. Book section near bottom
5. Logos of affiliate companies
6. Banner ads in the blog page
7. Light/dark?
8. Elements that move on mouse position and scroll
9. Write some copy
10. New Footer
11. "General" blog is too broad.  Better to break it down into more specific categories.
12. Less bloat in the code increases page loading speeds

## Challenges

The biggest challenge is to create a structure for the blog.  Instead of just having a list of posts with a category and ordered by latest date, an interesting blog is broken down into different sections by category and displayed differently rather than a uniform layout. 

For the purposes of this assignment, I copied a few articles, header images, excerpts and the first few paragraphics from the existing blog to demonstrate the reorganization. 

The purpose of takinga bootcamp at Lighthouse Labs is to learn a coding skill and landing a job. 

- Showcase students and their stories
- Give career advice and how to land a job

## Philosophy

Variety of content
separate based on category and topic

Oxygen over Elementor

Animation adds more personality to the design

Get classes and structure in place.  This helps developers style elements much more efficiently and it's better for the UX.

## Images

1. Sign-up

## JavaScript 

```js
document.querySelectorAll('.mover').forEach( mover => {	
	if( window.angular ) return;	
	window.addEventListener('mousemove', (e) => {		
		if( !calculating ) {			
			var calculating = setTimeout( () => {				
				var divisor = mover.getAttribute('speed') ?? 32;				
				var windowMouseX = (e.clientX - (document.documentElement.clientWidth / 2));
				var windowMouseY = (e.clientY - (document.documentElement.clientHeight / 2));
				var computedCSS = '';				
				var translateX = (windowMouseX / divisor) * -1;
				var translateY = (windowMouseY / divisor) * -1;
				computedCSS += 'transform: translateX(' + translateX + 'px) translateY(' + translateY + 'px);';
				mover.style.cssText = computedCSS;				
				clearTimeout(calculating);
			}, 100);			
		}		
	})	
})


window.addEventListener('scroll', () => {	
	if( window.angular ) return;	
	document.querySelectorAll('.spinner').forEach( spinner => {		
		spinner.style.cssText = 'transform: rotate(' + (-80 + (window.scrollY / 16)) + 'deg)';		
	})
```

## Image Accordion

```js
var ready = (callback) => {
	if (document.readyState != "loading") callback();
	else document.addEventListener("DOMContentLoaded", callback);
}

ready(() => {
	if(window.angular) return;
	
	document.querySelectorAll('.image-accordion__item:first-child').forEach( first => {
		first.classList.add('image-accordion__item--active');
	})
})

document.querySelectorAll('.image-accordion__item').forEach( item => {
	if( window.angular ) return;
	
	item.addEventListener('click', (event) => {
		event.target.parentElement.querySelector('.image-accordion__item--active').classList.remove('image-accordion__item--active');
		event.target.classList.add('image-accordion__item--active');
	})
})
```

```cs
.image-accordion__item {
	flex-grow: 1;
}

.image-accordion__item--active {
	flex-grow: 10;
}

.image-accordion__link {
	opacity: 1;
	transition: 0.3s opacity ease-in-out;
}

.image-accordion__item:not(.image-accordion__item--active) .image-accordion__link {
	opacity: 0;
}

body:not(.ng-scope) .image-accordion__item:not(.image-accordion__item--active) .image-accordion__details {
	pointer-events: none;
}
```
