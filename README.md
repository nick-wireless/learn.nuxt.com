# Episode 1 - Project Setup
PREAMBLE:
Hi, this is NH's notes on Antfu's video series, Learn.Nuxt.Com, which starts [here](https://www.youtube.com/live/49WXr6kVBVI?si=DO8OM44OG---GD6R).

About me: I have only podcast involvement in software (8 yrs + of listening with Changlog and Friends).  I have read some books and tinkered at home.  I wonder if I should have focused on software engineering in my career, rather than property & business.  (I love spending time in my 'virtual shed' with all the great tools of the web.  I particularly love the Vue & Nuxt ecosystem and heros within it).

My personal attraction to this series is I sit side saddle with a hero, to make a SASS product.  Something I might also get to one day.

What follows below are some more detailed notes taken directly from the episodes.  I follow the chapters set up by Antfu and tried to be a diligent student also linking to resources and doing a longer scan of them than Antfu typically needs to.  That said, as a beginner and as fitting this in between life, I'm keeping short and sharp as best I can.

So to help others, my notation and method described:
- H2 format is Antfu's headings, H3 sub-headings are my own grouping of concepts and sub-chapters to help my search & find later.
- [ this typically refers to code ] , meaning placing code comments between the brackets, which might also refer to the headline of the a key concept being discussed.
- Footnotes are a little extrapolation my end; usually interesting call outs based on readings of links provided, which may also interest you.
- (NH), refers to my own words, sometime taking liberty of interpretation of Antfu's words, in-line within Antfu's other comments.  These (NH) comments may jump to conclusions which would land the reader in the wrong spot.  (I call them out, as a 'reader beware', as I might be completely off track with these notes).

Re. actual code: well, the Video and Antfu's Github pushes are the real source of truth and great reference.  I've tried to add these to the summary too.

PR's / recommendation or learnings from others to this repo to improve its usefulness are welcome.  I'll try to keep in my own voice and I apologize in advance, for terrible grammar, spelling where it exists.

******
Footnote 1: a tip of the hat to deep thank you to Antfu.  The ecosystem and future of Vue, Nuxt, Vite, Nitro, UnoCss etc. seems bright to me.  To me, all involved appear as modern day demigods with superpowers and tremendous intuition to do great things.  Antfu personifies the new wave to a 'T' and as such I am choosing to peak into his workflows as a conscious choice to learn from such people.

It feels of a fashion, we are able to stand in the shadow (and on the shoulders) of modern day greats.  I only hope I can find the time to put some of their great tools to practical use too.  (I think I like the learning cycle more than the doing cycle).


## [0:00:00 Launch Of Project - General Discussion](https://www.youtube.com/live/49WXr6kVBVI?si=SAOWJIp038Dds7on)
Antfu is interested in how this process will play out.  We are building a Playground, inspired by the Svelte Learn Playground, see [here](https://learn.svelte.dev/tutorial/welcome-to-svelte) for that inspiration.  Antfu's programming style mixes UI implementation with Application logic.  Additional tweaks to a 'learning resouse' will be as follows:
(i) Consider use for reproducing bugs or issues environments for sharing.
(ii) Consider application to demostrate Nuxt's integration between SPA and SSR modes.
(iii) The architecture will showcase some of VueJS, Typscript and Nuxt's core packages, module and package workflow (and Antfu's workflow).

Antfu says, 'The actual build process is part of the process, so lets see how we go.'  Remember contributions and recommendations are welcome.

[## 0:06:20 Project Setup](https://www.youtube.com/watch?v=49WXr6kVBVI&t=380s)
- Often Antfu defaults to his ready made templates (Vitesse or Vitesse Nuxt), in this instance will build from scratch.
- Discussion: about Antfu's settings, for this has a link with all the info [[ antfu/use ]](https://github.com/antfu/use).
  - "windows.nativeTabs": true, ... in VSCode to get the project to a tab view (MacOS only).
  - [ ni ] in the terminal, is an alias to [ npm i ] or similar, however it will automatically choose the right package manager you are using in the project. See here for more details [[ antfu/ni ]](https://github.com/antfu/ni).

### Installing packages & setup
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



