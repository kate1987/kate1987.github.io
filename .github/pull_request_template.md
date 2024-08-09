# Documentation Style Guide

### Guideline 1 - Write Docs, Not Wikis
<details>
  <summary>
    Expand!
  </summary>
<br/>
  
* The documentation website is, for all intents and purposes, marketing material
* The Wiki is internal - it’s intended to transfer information between developers inside the company 
* The Documentation is external - it’s intended to convince developers outside the company that Lightrun is a solid product that can solve their problem (and then simply be helpful once they’re convinced)  

#### 👍  Awesome!

> Lightrun supports Python V2.7 and Python V3.6-3.9.

#### 👎  Less awesome...

> The python agent supports Python2.7 and Python3 (Subversions 3.6,3.7,3.8,3.9 are explicitly supported, **newer versions will probably work as well, but haven't been tested**).
</details>

### Guideline 2 - Write like you don’t know the product
<details>
  <summary>
    Expand!
  </summary>
<br/>
  
* When writing, imagine you are reading docs from a product you do not know intimately like you know Lightrun  

#### 👍 Awesome!

> Lightrun allows you to add snapshots - you can think of them as “non-breaking” breakpoints.

#### 👎 Less awesome...

> Lightrun allows you to add snapshots.
</details>

### Guideline 3 - Write step-by-step instructions, not scripts
<details>
  <summary>
    Expand!
  </summary>
<br/>
  
* When adding instructions, explain what each command in the way does or what each step in the way will cause

#### 👍 Awesome!


> 1. Clone the agent’s repo:
> 
>     ```bash
>     git clone https://github.com/athena-io/athena.git .
>     ```
> 
> 2. Open the agent’s source code folder:
> 
>     ```bash
>     cd athena/agent_src
>     ```
> 
> 3. Build the agent using the build script:
> 
>     ```bash
>     bash build.sh
>     ```

#### 👎 Less awesome...

> Build agent:
> 
> ```bash
> git clone https://github.com/athena-io/athena.git . &&
> cd athena/agent_src &&
> bash build.sh
> ```
</details>

### Guideline 4 - Links, Links, Links
<details>
  <summary>
    Expand!
  </summary>
<br/>
  
* Keep in mind that the users reading the docs are not always fully aware of EVERYTHING in the docs site
* Lead the way using smartly-placed links in actionable instructions

#### 👍 Awesome!

> View the output and [exceptions](https://example.com/1) directly [from the IDE](https://example.com/2) - or [from our app in the browser](https://example.com/3).

#### 👎 Less awesome...

> View the output and exceptions directly from the IDE - or from our app in the browser.
</details>

### Guideline 5 - When to Image
<details>
  <summary>
    Expand!
  </summary>
<br/>
  
* Generally speaking, screenshots are appropriate when the interaction with the GUI is either:
  * Not intuitive
  * Requires use of something the user doesn’t already know, like our management portal
* Refrain from adding screenshots in places code snippets will do - code we can copy and paste is always better than code in an image
* However, when (like in our onboarding flow) images are critical for understanding what to do, make sure to add them

#### 👍 Awesome!
```bash
java -jar lightrunc.jar list-agents
```

#### 👎 Less awesome...
![alt text](https://i.ibb.co/nCD5nK8/Docs-at-Lightrun-Google-Slides.png)
</details>

### Guideline 6 - How to Image
<details>
  <summary>
    Expand!
  </summary>
<br/>

* MkDocs supports HTML attributes
* We use the <figure> attribute to add images
* To add an image:
  * Add it to the assets/images folder with a descriptive name - i.e. `assets/images/webstorm-ide-plugin.png`
  * Insert it in the appropriate place using a relative path - note that the path is from the location of the .md file, not the eventual HTML file
  * Use the (default) `width=600`
  * Add a relevant caption

#### 👍 Awesome!

  ```html
 <figure>
    <img src="../assets/images/webstorm-ide-plugin.png" width="600" />
    <figcaption>The Lightrun WebStorm IDE Plugin</figcaption>
</figure>
```  
  </details>


