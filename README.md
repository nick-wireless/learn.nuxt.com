# Index

- [Episode 1 - Project Setup](#episode-1---project-setup)
- [Episode 2 - Nuxt Content & Resizable Panels](#episode-2---nuxt-content--resizable-panels)
- [Episode 3 - Pinia & Editor Refactors](#episode-3---pinia--editor-refactors)

***


PREAMBLE:
Hi, this is NH's notes on Antfu's video series, Learn.Nuxt.Com, which starts [here](https://www.youtube.com/live/49WXr6kVBVI?si=DO8OM44OG---GD6R).

About me: I have only podcast involvement in software (8 yrs + of listening with Changlog and Friends).  I have read some books and tinkered at home.  I wonder if I should have focused on software engineering in my career, rather than property & business.  (I love spending time in my 'virtual shed' with all the great tools of the web.  I particularly love the Vue & Nuxt ecosystem).

My personal attraction to this series is I sit side saddle with a hero, to make a SASS product.  Something I might also try to do by myself one day.

What follows below are some more detailed notes taken directly from the episodes.  I follow the chapters set up by Antfu and tried to be a diligent student also linking to resources and doing a longer scan of them than Antfu typically needs to.  That said, as a beginner and as fitting this in between life, I'm keeping short and sharp as best I can.

So to help others, my notation and method described:
- H2 format is Antfu's headings, H3 sub-headings are my own grouping of concepts and sub-chapters to help my search & find later.
- [ this typically refers to code ] , meaning placing code comments between the brackets, which might also refer to the headline of the a key concept being discussed.
- Footnotes are a little extrapolation my end; usually interesting call outs based on readings of links provided, which may also interest you.
- (NH), refers to my own words, sometime taking liberty of interpretation of Antfu's words, in-line within Antfu's other comments.  These (NH) comments may jump to conclusions which would land the reader in the wrong spot.  (I call them out, as a 'reader beware', as I might be completely off track with these notes).

Re. actual code: well, the Video and Antfu's Github pushes are the real source of truth and great reference.  I've tried to add these to the summary too.

PR's / recommendation or learnings from others to this repo to improve its usefulness, they are welcome.  I'll try to keep the writing in my own voice and I apologize in advance, for terrible grammar and spelling where it exists.

******
Footnote 1: a tip of the hat to deep thank you to Antfu.

To me the ecosystem and future of Vue, Nuxt, Vite, Nitro, UnoCss etc. seems bright.  To me, those involved appear as modern day demigods with superpowers and tremendous intuition & energy to do great things.  Antfu personifies the new wave and energy to a 'T' and as such I am choosing to peak into his workflows as a conscious choice to learn from such great people.

# Episode 1 - Project Setup

## [0:00:00 Launch Of Project - General Discussion](https://www.youtube.com/live/49WXr6kVBVI?si=SAOWJIp038Dds7on)
Antfu is interested in how this process will play out.  We are building a Playground, inspired by the Svelte Learn Playground, see [here](https://learn.svelte.dev/tutorial/welcome-to-svelte) for that inspiration.  Antfu's programming style mixes UI implementation with Application logic.  Additional tweaks to a 'learning resouse' will be as follows:
1. Consider use for reproducing bugs or issues environments for sharing.
2. Consider application to demostrate Nuxt's integration between SPA and SSR modes.
3. The architecture will showcase some of VueJS, Typscript and Nuxt's core packages, module and package workflow (and Antfu's workflow).

Antfu says, 'The actual build process is part of the process, so lets see how we go.'  Remember contributions and recommendations are welcome.

## [0:06:20 Project Setup](https://www.youtube.com/watch?v=49WXr6kVBVI&t=380s)
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


## [0:31:35 Basic Layouting](https://www.youtube.com/watch?v=49WXr6kVBVI&t=1895s)
- Note: good practice to use 2 words for component names, to avoid collision with standard html elements.  TheNav is a good example to avoid collision with <nav></nav>.

### [UnoCSS - simplifying first steps](https://www.youtube.com/live/49WXr6kVBVI?si=jOIzkOTPfJqjLYtM&t=2027)
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

## [0:58:14 Setup WebContainers](https://www.youtube.com/watch?v=49WXr6kVBVI&t=3494s)
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

## [2:02:12 Q&A](https://www.youtube.com/watch?v=49WXr6kVBVI&t=7332s)
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

# [Episode 2 - Nuxt Content & Resizable Panels](https://www.youtube.com/live/mDjI1uR-s-M?si=Nsvkq8rm9GlZ61r6)
Preamble: Anthony would love to progress the project together, feel free to jump in yourself.

Reviewing commits between videos:
- FitAddon from 'xterm-addon-fit', allows the terminal component to resize dynamically
- Repositioned color-mode button to the top.

Loads up page...
- Note, styles of booted 'nuxt project' have a glitch
    - Consider that file is there but reading as HTML not css.
    - Shows how to identify css location.
    - Park issue for now and revert later.
- Consider container & situation of starting server sessions within server sessions.  (Instead stop the un-intended spawning of these, to allow one instance of HLR).

## [0:06:50 UI Tweaks](https://www.youtube.com/live/mDjI1uR-s-M?si=gBGANUDenMikl8gC&t=405)

### [Discussion on how to implement a desing system](https://www.youtube.com/live/mDjI1uR-s-M?si=eF6M00ycU-F1wfqY&t=1279)
Reference the new Nuxt design scheme, see [here](https://nuxt.com/blog/new-website).
- Start by loading background preset shortcuts found in uno.config.ts, 'bg-base' in this instance input hash, 'bg-[#020420]'
- Discusses pros and cons of applying a bg to the layout.  Antfu's pref is to apply within app.vue, under the html or body tag.  In this way, is applied across all elements.
    - If chose to use @apply (from TailwindCss) to append then shows how this is supported: need to enable this functionality in UnoCSS through 'transformers', by adding 'transformerDirectives()', which essentially a means to call in, 'special syntax inside HTML'. 
    - However, syntax highlighting of vscode disagrees with this direction, so Antfu shows another built-in way from UnoCSS, '--uno: bg-base' which keeps css prompting of editor in line with expectations.
    - [Footnote: another exit door for @apply, is --at-apply, which also streamlines editor experience if you prefer.]
- Lets consider font use:
    - Usual way is to download specified weights and scripts, however UnoCSS has a helper here too.
    - Under presets, import then add presetWebFonts({}), which accepts an object to allow setup options.
      - The two options discussed: provider and fonts.
      - Provide is usually 'google', but there are others see below.
      - The fonts, allows assigning the order of application to the preset 'defaults'.
    - Having set them up, now find a place to apply them (like html / body, within app.vue... appended to the UnoCSS presets).

- Next, Antfu shows path to customize and use a custom svg in your project, in this instance taking a websource that isn't quite right and editing it for our use case.
    - Having downloaded the svg, setup in a .vue file within a standard template.
    - Viewbox is enough, so can remove height and width.
    - This is the 'Home Button' logo, so makes sense also to wrap in a NuxtLink component.


Interesting asides (exploring the links provided):
- [Font Bunny](https://bunny.net/fonts/) provide is a choice that prevents user tracking through adoption of font services.
- Nuxt Design upgrade, also implemented a ['Github Source Code']((https://nuxt.com/blog/new-website)) button, that allows you to quickly deepdive into the code being discussed in the documentation.

Commit: [/ feat: align with nuxt.com design /](https://github.com/nuxt/learn.nuxt.com/commit/ebf7293625c23ce57fc3918125f079ef4ebdb801)

## [0:36:20 Setup Nuxt Content](https://www.youtube.com/live/mDjI1uR-s-M?si=9tcwjc9XRu8xbmrH&t=2181)
- Confirms Nuxt Content was added in earlier session, next follow docs... ... [Nuxt Content Docs](https://content.nuxt.com/get-started/installation)
- Add within a new folder, Content and index.md file, which is the start of the content presented, beginning with the index file.
- Under pages/[...slug].vue add a <ContentDoc /> component was the example from the docs website, however Antfu shows how can call in a page directly with simply the <ContentDoc /> component.
- Next: consider how you might apply styles to this component...
    - Not so obvious from the Nuxt Content Docs, so instead reverted to [UnoCSS Typography](https://unocss.dev/presets/typography) and use those tools.
- Shows how pages directly dynamically establishes routes for the content in the Content folder, by renaming or introducing the page [...slug].vue.

Footnotes & interesting asides (exploring the links provided):
- UnoCSS Typography has a great set of [preset colors](https://unocss.dev/presets/typography#colors) that can be applied to make your fonts look professional.
- Also, has ability to introduce 'relative sizes' of e.g. p vs h1!

Commit: / feat: integrate '@nuxt/content' /


## [0:43:42 Struggling with WebContainers](https://www.youtube.com/live/mDjI1uR-s-M?si=tdZBoCbLjp3aAhjG&t=2623)
- Next, lets make the playground represent files from focused project in the playground:
    - Within /templates/basic/app.vue - provide for a hello world, to update (instead of the slot) - works.
- Obvious, that currently outside 'color-mode' selection is not also updating internal playgroud (in sync), so lets consider that:
    - Rather than replicating 'color-mode' inside, consider css variable... ...?
    - The playground is in it's own iframe, so shows how $0 can access that element (ref found in dev tools by selecting in) - terminal also can access that by $0.
    - Experimenting:
        - within (process.client), add an eventlistener, passing in an (e).
        - As consider needs to fire after server is ready, simplify in first instance to fire from button click.
            - Notice: not getting to process.client in the first instance...
              - Find that the entry.js, delivers HTML vs a Nuxt App.
              - Simplify server, to dissable server side rendering (SSR) in nuxt.config.js.
              - Problem shoot by swapping out Nuxt with Vite - appears to work on client side.
              - Problem shoot by swapping out Vite with Nitro.
                - Nitro works directly, however not within a container.
                  - Oh... because grabbing only part of the Nitro set of files, fix that bug.
                  - OK... now observe, the files should be imported in a flat version for Stackblitz.'
                  - Writes the method to flatten the file system.
              - Next, shows how to export 'globFilesToWebContainerFs', withing composables, to call into the component at hand.

Commit: / feat: support mounted nested folder to WC /

- Back to original problem, Nuxt representing in WebContainer...
    - Errors present, test by regressing Nitro to an earlier version, in case due to latest.
    - Realize, with "overides" to specify the "nitropack" version, use "~2.7" not "^2.7" to prevent auto update.
    - Next... explore a Stackblitz example booting a Nuxt preview instance.
    - Consider... HTTPS, for load setting for Nitro... implement.

// PARK ... will ask around and return later.

Footnote, interesting asides:
- In terminal, can access window.useNuxtApp() in the session


## [1:41:00 Resizable Panels](https://www.youtube.com/live/mDjI1uR-s-M?si=RUwKWggLfJiztGfv&t=6062)
- Next, lets implement resizable windows.
- An old library that is still used for this is ['Splitpanes'](https://github.com/antoniandre/splitpanes)
    - Follows documentation for importing.
    - Styles added after the uno.css import, however not showing up... ...
      - Decide to add a dedicated 'styles/overides.css' file to target and style the divider.
      - Notice, when dragging it, the grip of the mouse can lose the edge.  To work around this, use point-event null.
        - The library contemplates this and has events of 'resize and resized' to allocate to 'start and end' respectively.
        - Then... conditionally add to the Playground (the listening component) not to listen to cursor event when isDragging.
    - Lets preserver the size of the window after resizing to prevent 'refresh' resetting the window.
      - Shows how to create your own limited type for a variable after investigating the output from the library.
      - Apply the width % to leftSize variable created.
      - Shows best practice to 'persist this value' with useLocalStorage() function from Nuxt, with a key and deafault.
      - Consider if need animation to assist UX, decide not, so remove it from the styled feature.
    - Next... apply similar styling to the horizontal dividers.
    - NOTE: we could repeat the 'isDragging' for his component as well, however Antfu instead shows how to extract it as a composable, within a state.ts file.
      - Rather than exporting a ref, shows how to export a function (which is now a composable).
      - This is an interesting pattern, when [applying the composable](https://www.youtube.com/live/mDjI1uR-s-M?si=bTZsAVfa9WRZtcAX&t=7427), through the refactor.

Commit: / feat: support resizable panels /


## [2:10:00 Chat & Tools Sharing](https://www.youtube.com/live/mDjI1uR-s-M?si=44casB-Nwwk6fqam&t=7802)
- Close Playground coding session and open up for general chat about process, streaming and the tooling used.

General chat:
Mostly talking about the tooling described in [Github, Antfu Use Page](https://github.com/antfu/use).
- Re. Presets for UnoCSS, yes could autoimport the lot, however like also to allow people to consider and choose what they are using for each project.
- Discussed preferences of various settings in VSCode.
- Generally speaking, I use CMD pallette for the general dictionary of shortcuts vs setting specific keyboard shortcuts.
- Antfu uses eslint for linting and formatting and describes why [here](https://antfu.me/posts/why-not-prettier).  Essentially, allows line by line control over how things are handled (with highlevel options).

### From the audience:
- To flip between start and end of open brackets: CMD + Shift + \
- To jump to that line number: CMD + P, then : with line number

Deeper dive topics:

### Eslint settings for wrapping of lists:
- Eslint, customized his own prettier formatting preference re. first items::
    - Can change the arrangement 'all on one line' vs 'vertical list' of items, but setting preference on the first item.
    - Look for rule drafting in []'consistent-list-newline'](https://github.com/antfu/eslint-plugin-antfu/blob/main/src/rules/consistent-list-newline.md)

### Searching existing alternate code bases, while in flow:
- One good efficiency hack Antfu uses with the Tab functionality available in MacOS & VSCode is CNT + R (for recent) to look (or search through) previously opened projects.
- Tip: consider CNT + R && CMD + Enter on selected project, opens in a new tab.
    - Great for setting up workspaces (learning from other projects) or
    - For opening a reference project to review before writing your own.
- CMD + P, allows you to search for files within the project.

### [.zshrc](https://github.com/antfu/dotfiles/blob/main/.zshrc)
- Highlights a long list of aliases, within zsh, for node use.
- Simplified the 'standard call' by also simplifying the call to nr, which auto-selects the right package manager.
- (Notice, all aliases are simply one letter or so).
- Hub (hub.github.com) vs cli.github.com discussion.
- Clonei ... use i (for my code master folder) or f (for forked code master)
    - clonei thus, puts the code in the right place from whereever I am (and open it)
    - clonef, puts into the fork folder and opens it.
    - cloner - puts into reproduction folder and opens it.
    - codei vite - is a helper along the same lines, 'knowing you have a project, opens it quickly from whereever, in this case vite'.

### Reviewing code hacks...
[Piece together of the above... having loaded the target projects in the various folders]
- pr function, with the number... when inside the repo, opens the PR in the code editor.
- then 'main' to get back out.


# Episode 3 - Pinia & Editor & Refactors

## [0:00:00 Prepare]()
## [0:08:15 Explain issue from the last episode](https://www.youtube.com/live/B7JJP-vgImM?si=tQle-dxTdfvKLK_q&t=499)
About previous episode bug / stopper:
- Antfu began investigating but guzumped by 2 of the community members following along (both submitting PRs at same time).
- Nub of issue is that Nitro initiates a number of servers and the WebContainer listen's to the last one.
- Discussed nominating a port (env), or selecting the smallest number.  For now going with hard-coded 3000 port.

This code is found in merging of Issue 12 and 13, [here](https://github.com/nuxt/learn.nuxt.com/pull/13).


## [0:16:07 Merged PRs catch up](https://www.youtube.com/live/B7JJP-vgImM?si=8ayPREGERa-gFCVy&t=986)
Discuss other merged PRs, first up discussing community contributions:
- Local Cookie: switched, from useLocalStorage('nuxt-playground-panel-left') to a usePanelCookie (composable...) details [here](https://github.com/nuxt/learn.nuxt.com/pull/14).
- Npmrc: import.meta.glob, doesn't include .* files explicitly, [so consider adding](https://github.com/nuxt/learn.nuxt.com/pull/11)?  (Antfu will revisit later).
- Switch Color Styling: considered [dynamic styling](https://github.com/nuxt/learn.nuxt.com/pull/17) for change of color-mode.  Antfu decides doesn't fit current use case, but good demonstration of code so calling it out, in case useful for others.
- Panel sizing: avoiding a bug if one panel is resized to 0, [here](https://github.com/nuxt/learn.nuxt.com/pull/18).

Next, discussing those UI changes Antfu made in between sessions:
- Updated, such that there is a single svg for logo.
- Improved dividers, to be more subtle.
- Added headers to each section.

Explored community ideas on design discussed:
- Adding in preset unocss for Playground.  Antfu wishes to keep lean, and not add in too many dependencies, while keeping un-opinionated for projects that are loaded.
- Concept, a Search & Refresh bar: Antfu checkedout PR and discussed merits of design and direction, demonstrating how he merges such a PR:
    - A consideration is there is a difference between 'hard navigation' and 'soft navigation', where 'soft navigation' is referring to the navigation enabled by VueRouter (and doesn't reload the whole page).
    - Implements with a simplified design.
See [here](https://github.com/nuxt/learn.nuxt.com/pull/21) for that PR merger. 

## [0:35:41 Refactor components](https://www.youtube.com/live/B7JJP-vgImM?si=uVrJ2H991P-_8Q5c&t=2142)
Lets revisit the .client component:
- Antfu notes because the preview pane is rendering client only, there is a noticeable delay in the rendering of the page.
- Considering a different approaches, with a <PanelPreview> component:
    i. Pulling the 'initialization' of the panes on RHS to be later, while the painting of the blocks are prepared earlier.
    ii. Pulling logic from the component, to allow more easily understanding what is going on.
- Interesting turn, is that <PanelPrivew> shares state object (:stream="stream") from the preview into the terminal pane... so consider options for that:
    - One way is again, falling back to useState() composable as part of a new function for the purpose of sharing (such as e.g. useTermianStream), however this feels a temporary fix, so in instead [*reaching for Pinia*](https://www.youtube.com/live/B7JJP-vgImM?si=0HDyemEOq9bnxLUt&t=2591).
    - Putting finer control to size of panes, noting horizontal spacing and vertical spacing are independent, create two different values to track.
    - Thus Antfu, shows how .client render the components still relevant, however the server now provides the content to hydrate within these components.
        - Showing how the hydration is having difficulty finding the parent element.
        - Try various ways of linking to element and resolve by using nextTick().
        - Perhaps a better way is for a watch() component that stops after the element has appear.

Next, lets also want the server boot logic to be in its own composable... lets pause and consider all our todos currently.

## [0:56:09 Listing TODOs](https://www.youtube.com/live/B7JJP-vgImM?si=-wjb0OHtqMh_oZLk&t=3372)
- Antfu lists 6 todo items, from adding Pinia, to syncing styles.
- Then considers order of todos, as the order can help with the following component creation.
- Monaco Module - discussed as option for including.  Antfu, decides to roll his own as keen to manage the integrations directly.
    - This lead to exploration of the SFC Vue Playrgound, which has type support and a Monaco editor implementation.
    - However, lets avoid implementing another runtime instance of Vue when we have the Nuxt infrastructure already. 
- Where does this leave us? ... Well, instead of implementing Monaco (which could take weeks), lets focus on getting an editor in its simplest form working.

## [1:06:15 Virtual File Structure](https://www.youtube.com/live/B7JJP-vgImM?si=ciEFzvFG0dUn3i6f&t=3979)
OK... so lets do the refactor of the composable and hook up basic editing in the webcontainer:
    - Focus, on startDevServer(), placing within playground.ts.
    - Consider if functions are flat, async or mounted within PanelPreview.client.vue.
Commit: / refactor: moving and dividing some parts / [code here](https://github.com/nuxt/learn.nuxt.com/commit/7daf1fed3c788a6dc174127f1b732be5b0354a3b?diff=unified&w=0)

[Next](https://www.youtube.com/live/B7JJP-vgImM?si=C7C8LSEmkIdrlt5t&t=4686)... lets consider the file we are writing to, it might be any of a number, so lets consider a virtual file system:
- First up, imagining a class File, with all the components.
  - Detailed outline of the type and file structure of the files now considered.
  - Key: made as a function loadFiles(), so that can load multiple times without mutating it.
  - Or... could also make reactive... with a getter() in the File...?

[Footnote](https://www.youtube.com/live/B7JJP-vgImM?si=0lDMB38kjCz4qE2J&t=5292): types were not 'reading in vscode descriptions' through the project, so updated nuxt.config.js to enable it so that it could.


## [1:44:00 Explain Vue reactivity unwraps](https://www.youtube.com/live/B7JJP-vgImM?si=6aY3gTjk3u97bFL6&t=3980)
[* Real world example of ref v. Reference v. shallowRef, with explanation *]()
- Note: to access a ref, which is nested, this value isn't unwrapped automatically, so need to use .value to access it.
- Considered using reactive() instead, which then discards use of .value as is automatically unwrapped.

- Noting that, however using useState with nested values we ran into roadblocks.  Antfu explains with the Vue SFC playground the issues at play.
- Solution: can markRaw({}) the object in order to avoid useState getting too handson with trying to assist us with a solution.

## [1:58:40 Basic Editor and HMR](https://www.youtube.com/live/B7JJP-vgImM?si=ctrpHptzFY_2rHoq&t=7123)
Consider props and defineProps, to pass in the file to be used in the editor.
- In this instance to pass in the files selected, why not instead start with defaults?  Antfu shows, props = withDefaults pattern.
- Demonstrates simple presentation of files with a preview pane.
- (of-auto, shortcut for overflow-auto in the viewport)
- Next, shows how can throttledWatch the files for changes - from VueUse.
- Demonstrates, 'text-primary' highlighting of current file, with the simple presets of UnoCSS set up in earlier classes.

Commit: / feat: introduce `File` structure and add basic editor / [code here](https://github.com/nuxt/learn.nuxt.com/commit/0d1bc13e4aef14a0967763c1d6671e17caa09298)

## [2:15:00 Explain Vue defineProps](https://www.youtube.com/live/B7JJP-vgImM?si=VlZyM6Q6WdSkfD8e&t=8108)
Antfu runs through the syntax of various ways of declaring Props.

## [2:25:00 Refactor to Pinia](https://www.youtube.com/live/B7JJP-vgImM?si=kMmfgBgh07iL_rX4&t=8702)
Antfu gets on a march and explains the excitement of working through a clear list of todos for a new project.  (Getting the mix just right between not too easy, not too hot),
- Setting up Pinia, noting... Antfu, has never used it before, so learning along with us.
- A good opportunity to show the Nuxt Devtool setup.  Devtools allows a GUI for finding module and installing.  The install process also forecasts what changes will be made.
  - However, cross origin policies blocked the install, so reverted to '*' accepting all origins.
  - Devtools, works now but ....

Bug: identify cross-origin headers need to be specifically specified for the webcontainer, however this appears to be at odds with allowing devtools to work.  (Will park and come back to this).

*###Pinia*
- Antfu, starts by playing around to experiment on how the store is initiated if called in components on the web or client.
- Considers moving the usePlayground into the store and then typing the environments.
- My utilising the mount() function on the client side, that also provides some simplification between concerns re. server vs client.

Antfu's thinking, 'Pinia, helps share state while bing SSR friendly'.

Next let's consider the individual ui elements, some make sense to simply implement in state (such as isPanelDragging), whereas the individual values of the panel sizes would be better passed together.
- Looked at creating own {}, including Json.stringify to create own inputs, however
- Discovered Nuxt's composable useCookie automatically serializes and deserialize, docs revealed [here](https://nuxt.com/docs/api/composables/use-cookie).
- Antfu showed the 'traditional way' pre-Nuxt, then simplifies the code to rely on Nuxt's built in composables, which simplifies the approach a lot.

Commit: / feat: refactor using pinia / [code here](https://github.com/nuxt/learn.nuxt.com/commit/9913b51d47dedfe6c0681568e309aa02b24020a4)

Observation: the mount() is in the store, however we only want to call and operate this once... ... so lets move it to the webcontainer.  Antfu - shows refactor on this.

Qu: why useCookie over useLocalStorage?  Ans: because we want the opportunity of the state to come from the server.



