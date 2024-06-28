# CYBERFICTION

This project demonstrates a CYBERFICTION using Locomotive Scroll and GSAP (GreenSock Animation Platform). It includes a series of images that are animated as the user scrolls through the page, along with pinned sections that remain fixed during scrolling.

## Table of Contents
- Demo
- Installation
- Usage
- Code Overview
- Technologies Used
- ScreenShot

## Demo
You can see a live demo of the project here.

## Installation
#### 1. Clone the repository:
```markdown
git clone https://github.com/sahilsingh12221802/CYBERFICTION.git
```

#### 2. Navigate to the project directory:
```markdown
cd CYBERFICTION
```

#### 3. Open `index.html` in your browser to see the project in action.


## Usage
To use this project, you need to ensure you have the required assets in the assets directory. The images should be named sequentially (e.g., male0001.png, male0002.png, ..., male0300.png).

## Code Overview
### HTML
The `index.html` file sets up the basic structure of the webpage with sections for navigation, the main content, and the canvas element where images are rendered.

### CSS
The `style.css` file contains styles for the layout and appearance of the page. It ensures that the sections take up the full viewport and that the canvas is positioned correctly.

### JavaScript
The `script.js` file includes the following functionalities:
- **Locomotive Scroll Initialization:** Smooth scrolling and scroll event handling.
- **GSAP ScrollTrigger:** Synchronizes the animation with the scroll position.
- **Canvas Rendering:** Loads and renders images on the canvas based on the scroll position.

### Key Functions and Code Snippets
#### 1. Locomotive Scroll Setup:
```javascript
function locomotive() {
    gsap.registerPlugin(ScrollTrigger);
    const locoScroll = new LocomotiveScroll({
        el: document.querySelector("#main"),
        smooth: true,
    });
    locoScroll.on("scroll", ScrollTrigger.update);
    ScrollTrigger.scrollerProxy("#main", {
        scrollTop(value) {
            return arguments.length ? locoScroll.scrollTo(value, 0, 0) : locoScroll.scroll.instance.scroll.y;
        },
        getBoundingClientRect() {
            return { top: 0, left: 0, width: window.innerWidth, height: window.innerHeight };
        },
        pinType: document.querySelector("#main").style.transform ? "transform" : "fixed",
    });
    ScrollTrigger.addEventListener("refresh", () => locoScroll.update());
    ScrollTrigger.refresh();
}
locomotive();
```

#### 2. Canvas Image Sequence Setup:
```javascript
const canvas = document.querySelector("canvas");
const context = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

window.addEventListener("resize", function () {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    render();
});

function files(index) {
    var data = `assets/male0001.png assets/male0002.png ... assets/male0300.png`;
    return data.split("\n")[index];
}

const frameCount = 300;
const images = [];
const imageSeq = { frame: 1 };

for (let i = 0; i < frameCount; i++) {
    const img = new Image();
    img.src = files(i);
    images.push(img);
}

gsap.to(imageSeq, {
    frame: frameCount - 1,
    snap: "frame",
    ease: `none`,
    scrollTrigger: {
        scrub: 0.15,
        trigger: `#page>canvas`,
        start: `top top`,
        end: `600% top`,
        scroller: `#main`,
    },
    onUpdate: render,
});

images[1].onload = render;

function render() {
    scaleImage(images[imageSeq.frame], context);
}

function scaleImage(img, ctx) {
    var canvas = ctx.canvas;
    var hRatio = canvas.width / img.width;
    var vRatio = canvas.height / img.height;
    var ratio = Math.max(hRatio, vRatio);
    var centerShift_x = (canvas.width - img.width * ratio) / 2;
    var centerShift_y = (canvas.height - img.height * ratio) / 2;
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.drawImage(img, 0, 0, img.width, img.height, centerShift_x, centerShift_y, img.width * ratio, img.height * ratio);
}
ScrollTrigger.create({
    trigger: "#page>canvas",
    pin: true,
    scroller: `#main`,
    start: `top top`,
    end: `600% top`,
});
```

#### 3. Section Pinning:
```javascript
gsap.to("#page1", {
    scrollTrigger: {
        trigger: `#page1`,
        start: `top top`,
        end: `bottom top`,
        pin: true,
        scroller: `#main`,
    }
});
gsap.to("#page2", {
    scrollTrigger: {
        trigger: `#page2`,
        start: `top top`,
        end: `bottom top`,
        pin: true,
        scroller: `#main`,
    }
});
gsap.to("#page3", {
    scrollTrigger: {
        trigger: `#page3`,
        start: `top top`,
        end: `bottom top`,
        pin: true,
        scroller: `#main`,
    }
});
```

## Technologies Used
- HTML
- CSS
- JavaScript
- Locomotive Scroll
- GSAP (GreenSock Animation Platform)

## ScreenShot
<img width="440" alt="Screenshot 2024-06-28 at 10 17 28 PM" src="https://github.com/sahilsingh12221802/CYBERFICTION/assets/114878612/e25f6d1c-5732-43e4-a7a6-d3d606182042">

<img width="440" alt="Screenshot 2024-06-28 at 10 17 38 PM" src="https://github.com/sahilsingh12221802/CYBERFICTION/assets/114878612/e8a1ca35-b9d3-4ccc-b383-d591e7562ce1">

<img width="440" alt="Screenshot 2024-06-28 at 10 17 49 PM" src="https://github.com/sahilsingh12221802/CYBERFICTION/assets/114878612/89f8759b-1006-4d45-b0dd-d055af4db76e">

<img width="440" alt="Screenshot 2024-06-28 at 10 17 58 PM" src="https://github.com/sahilsingh12221802/CYBERFICTION/assets/114878612/80b5fb5d-e1ba-448c-abc7-1cd87ca249af">
