#Episode 1 - Project Setup

[0:00:00 Intro](https://www.youtube.com/live/49WXr6kVBVI?si=feG_wYtmS9d7DKub)
- This project, very inspired by [Learn.svelte.dev](https://learn.svelte.dev).
- Stackblitz's webcontainer is another key component.
- Will likely have its own design style and also will add a few other objectives:
  - Allow for reproduction of issues.
  - Extensible (with other module systems).
  - Could download & run as a standalone app.

Moreover, the actual build process is part of the process for learning and demonstrating Nuxt, so lets see how we go.

[0:06:20 Project Setup](https://www.youtube.com/watch?v=49WXr6kVBVI&t=380s)
- Often Antfu defaults to his ready made templates (Vitesse or Vitesse Nuxt), in this instance will build from scratch.
- Discussion: about Antfu's settings, for this has a link with all the info [[ antfu/use ]](https://github.com/antfu/use).
  - "windows.nativeTabs": true, ... in VSCode to get the project to a tab view (MacOS only).
  - [ ni ] in the terminal, is an alias to [ npm i ] or similar, however it will automatically choose the right package manager you are using in the project. See here for more details [[ antfu/ni ]](https://github.com/antfu/ni).

- Antfu follow documentation sites and implements from scratch for this project.
  - [Nuxt docs](https://nuxt.com/docs/getting-started/installation#new-project) - choosing [ npx nuxi-latest init learn.nuxt.com ] 
  - [Adding Modules](https://nuxt.com/blog/v3-8#%EF%B8%8F-nitro-v27) - chosing [ nuxi module add <module-name> ].
    - Adding, @vueuse/nuxt
    - Adding, @unocss/nuxt
    - Adding, @nuxt/content
    - Adding, @nuxtjs/color-mode
  - Adding Linting, see below for more details.
Along the way, Antfu shows how tests the success of the installs.

### [UnoCSS](https://www.youtube.com/live/49WXr6kVBVI?si=DRTuSN2L_Ps10DU3&t=1022)
[UnoCSS Docs Here](https://unocss.dev/presets/uno)
- Begins with a uno.config.ts file under root directory.  (Typescript should inteli-sense the options in your project.)
- A TailwindCSS alternative with more customisation.
  - Presets: [] - examples provied:
    - presetUno, the defaults (however does not restyle html elements, look to reset below)
    - presetIcons, allows to use icons as attributes
    - presetAttributify, allows direct writing of classes as attributes, with super powers. ***
  - Within App.vue, add the [ import '@unocss/reset/tailwind'] to reset the html elements.  (Allows your library to have greater consistency across a variety of browsers.)

*** Footnote: to me it appears it is like using BODMAS (bracket) notation in maths, only instead with named attributes outside equals, such as p="y-2 x-4", or font="mono light".

### [Nuxt Color-mode](https://www.youtube.com/live/49WXr6kVBVI?si=dFctbP0EdW3_T415&t=1171)
- Discussion: difference between nuxtjs/color-mode and vueUse, color-mode... the first is SSR compatible (as persists state via cookie that can be passed to server), helps with smarts behind hydration sent down the line.
- Begin in script setup initialize a variable to useColorMode().
  - Actually, first also needs, nuxt.config.ts to have additon of [ colorMode: { classSuffix: '' } ].

### [ESLint Formatting](https://www.youtube.com/live/49WXr6kVBVI?si=nvIzUI1oTPAeaJt3&t=1579)
- [ npx @antfu/eslint-config@latest ] - to install Antfu's eslint config.
- Then add script 1, [ "lint": "eslint ." ] to package.json.
- Then add script 2, [ "format": "eslint . --fix" ] to package.json.
  - Remember to ni (install) and restart editor.
  - Tip: CMD-P, Restart Extension Host, this restarts the setup of extensions within vscode to activate.

Discussion: about process, Antfu likes to work on UI with Logic in an iterative process (mixed together), this is the approach we'll adopt here too.

[0:31:35 Basic Layouting](https://www.youtube.com/watch?v=49WXr6kVBVI&t=1895s)
- Note: good practice to use 2 words for component names, to avoid collision with standard html elements.  TheNav is a good example to avoid collision with <nav></nav>.

### UnoCSS - simplifying first steps
- Antfu, shows practical application of layouts.
  - Layout of SPA, will take full screen, with the panels within scrollable, so set layout for full screen.
  - [ p4 ] is convention for 1rem.
  - [ grid-cols-[1fr_2fr] ] is convention for 1fr 2fr (fractional application of space) in UnoCSS leading to 2 cols.
  - Antfu, likes to apply opacity configs to e.g. border-gray:50.
- Antfu's personal preference is to pre-define tokens, or shortcuts for use in a design system.  These are aliases.  Therefore, consider the name: border-base, as a token instead pointed to the configuration border-gray:50.
  - The location UnoCSS puts these is [ shortcuts: { 'border-base': 'border-gray-50' } ].
  - Note, however, we can give this border-base even more power as a token.
    - Now, with this paradigm it is also possible to extra token specificity: 'border-gray-50 dark:border-red ', creating a responsive color for color-mode.
    - Benefits is that this is applied across the app consistently (and keeps code a little DRYer).
  
### [Logos & SVGs - simplifying first steps](https://www.youtube.com/live/49WXr6kVBVI?si=G9sIj16mJaYG8FU_&t=2710)
[icones.js.org](https://icones.js.org/)
- Demonstrates his method of using icons.
- With presetIcons(), can add icons as attributes.
  - Note, first step is to install the collection referenced.
    - Antfu demonstrates how to install a single iconset from icones.js.org.
    - Then shows how to install all the icon sets [ ni -D @iconify/json ].
    - 'You can used as a button or anything', meaning depending on the element wrapping the attribute, the svg can be used in any context you want.
- Inline classes... Antfu added additional functionality such that can drop the class="" syntax and simply inline the attributes.
  - Thus introducing also the 'grouping' of attributes, see presetAttributify notes above, [video example here](https://www.youtube.com/live/49WXr6kVBVI?si=RbIVecKtN9qeJRbx&t=3084).
- Antfu pulls all together with example of styling the github icon, with a hover effect.
- NuxtLink, swapped out as a more proformant option to <a></a> tag.
  - Soft routing enabled (Vue router loading vs. full page refresh).

Commit: [[ / feat: basic layout / ]](https://github.com/nuxt/learn.nuxt.com/commit/95753c559964dea1f9f99a0ac0f118876918873b)

[0:58:14 Setup WebContainers](https://www.youtube.com/watch?v=49WXr6kVBVI&t=3494s)
Reference Sites: [WebContainers.io](https://webcontainers.io/), [XTerm.JS](https://xtermjs.org/), [.getReader()](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/getReader)
- Antfu, follows documentation to implement a webcontainer.
- Documentation states warning, 'call only once'... Antfu, considers and sets up: [ /composables/webContainer.ts ]
  - Sets up guard to run only once.
  - Another term about what are coding: 'creating a singleton' pattern.
  - Consider the SPA vs SSR dynamics of Nuxt, consider also a good idea to use [ .client.vue ] on ThePlayground component, to ensure only run there.
- Webcontainers needs special headers enabled... Antfu, hunts around and feels the right place is to put within the Nitro server.
  - Problem shoots to represent first instance load of container.
    - [ npm script setup... ], needed to have the 'package.json', include [ script: { dev: 'nuxt dev'}].
    - [ watchEffect(()=>{})] , used in this instance to set the iframe.value.src (only after present), problem shooting js runtime getting ahead of itself.
- Progress Status: lets improve to move out of console and into UI.
  - Includes, spinner, v-show and demonstrate some more UnoCSS magic.

- Antfu, now considers Terminal output [here](https://www.youtube.com/live/49WXr6kVBVI?si=MBrzngNyMIkb-hEG&t=5075).
  - Considers 'output' vs 'stream'.
  - Jumps directly to xterm implementation.
    - [ const root = ref< HTMLDivElement>() ] - for anchoring an output, in this case for the output, terminal.open(root.value!).
    - Simplifies 'write to' methods to a watch(()=>{}), that takes the string and [ .pipeTo(stream) ], to add to it.
    - Includes imported style sheet for XTerm.
    - Problem shoots, exposing visibility of <TerminalOutput> below <ThePlayground>.
  - Observes, now visible.  Antfu, is wondering if the later part of stream [ stream.value = devProcess.output ] is appended.
  - Need a package.log: to speed up the webcontainer.
    - Therefore, creates a basic template for the package.log outputs (excluding node modules).
    - Considers reader again, this time writing... [ s?.getReader().read().then((done, value) => {})] ... and variations to fix this (introducing recursive behavior).

Commit: [/ feat: basic web container working /](https://github.com/nuxt/learn.nuxt.com/commit/868546a4e0610dff846233f936197bdfb8dc134b) 

[2:02:12 Q&A](https://www.youtube.com/watch?v=49WXr6kVBVI&t=7332s)
- Antfu discusses contribution standards (it would be great if you help out):
  - (i) Create an issue first.
  - (ii) Make PR as minimal as possible, so we can move forward.
  - (iii) Plan to review PRs in the live-stream.

- Open floor for Q&A:
  - nativeTabs (discussion): can drag them out (to be independent), it possible to open projects directly.
  - Iconify IntelliSense: a plugin code to show pictorially the icons in VSCode.
  - Held a poll on which font views enjoy most: Monaspace Krypton v Input Mono.
  - Roadmap: ESLint (to enable React & Svelte plugins) a backburner project, but will let you know when done.
  - Review first contribution: about async and _webContainer instance.  Very good feedback and quick, thank you!



