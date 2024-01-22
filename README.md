# Index

- [Episode 1 - Project Setup](#episode-1---project-setup)
- [Episode 2 - Nuxt Content & Resizable Panels](#episode-2---nuxt-content--resizable-panels)
- [Episode 3 - Pinia & Editor Refactors](#episode-3---pinia--editor-refactors)
- [Episode 4 - Frame Communications](#episode-4---frame-communications)
- [Episode 5 - Frame Communications](#episode-5---terminal0-panel-&-download-zip)

---

PREAMBLE:
Hi, this is NH's notes on Antfu's video series, Learn.Nuxt.Com, which starts [here](https://www.youtube.com/live/49WXr6kVBVI?si=DO8OM44OG---GD6R).

About me: I have only podcast involvement in software (8 yrs + of listening with Changlog and Friends). I have read some books and tinkered at home. I wonder if I should have focused on software engineering in my career, rather than property & business. (I love spending time in my 'virtual shed' with all the great tools of the web. I particularly love the Vue & Nuxt ecosystem).

My personal attraction to this series is we are invited to sit virtually side saddle with a web hero, Anthony Fu (Antfu), to make a SASS product. This is something I'd also like to do one day, so am doing a deep dive on his coding practices.

What follows below are some more detailed notes taken directly from the episodes. I follow the chapter structure set up by Antfu and tried to be a diligent student also linking to resources and doing a longer scan of them than Antfu typically needs to. That said, as a beginner and fitting this in between life, I'm keeping short and sharp as best I can.

To help others, my note taking notation and method described is described here:

- H2 format is Antfu's headings, H3 sub-headings are my own grouping of concepts and sub-chapters to help my search & find later.
- `this typically refers to code` and might also refer to the headline of the a key concept being discussed.
- Footnotes are a little extrapolation my end; usually interesting call outs based on readings of links provided, which may also interest you.
- (NH), refers to my own words, sometime taking liberty of interpretation of Antfu's words, in-line within Antfu's other comments. These (NH) comments may jump to conclusions which would land the reader in the wrong spot. (I call them out, as a 'reader beware', as I might be completely off track with these notes).

Re. actual code: well, the Video and Antfu's Github pushes are the real source of truth and great reference. I've tried to add these to the summary too.

PR's / recommendation or learnings from others to this repo to improve its usefulness, they are welcome. I'll try to keep the writing in my own voice and I apologize in advance, for terrible grammar and spelling where it exists.

---

Footnote 1: a tip of the hat and deep thank you to Antfu.

To me the ecosystem and future of Vue, Nuxt, Vite, Nitro, UnoCss etc. is bright. In my view, those involved appear as modern day demigods with superpowers and tremendous intuition & energy to do great things.

Antfu personifies the new wave of leaders and energy perfectly, his art (software) is impressive and his output is testomony in my mind to the beautiful online-tools he has made and chosen himself. Thank you Anthony, and thank you to all the leaders (Evan, Sebastian, Daniel etc) who came before to give us all momentum!

---

# Episode 1 - Project Setup

## [0:00:00 Launch Of Project - General Discussion](https://www.youtube.com/live/49WXr6kVBVI?si=SAOWJIp038Dds7on)

Antfu is interested in how this process will play out. We are building a Playground, inspired by the Svelte Learn Playground, see [here](https://learn.svelte.dev/tutorial/welcome-to-svelte) for that inspiration. Antfu's programming style mixes UI implementation with Application logic. Additional tweaks to a 'learning resouse' will be as follows:

1. Consider use for reproducing bugs or issues environments for sharing.
2. Consider application to demostrate Nuxt's integration between SPA and SSR modes.
3. The architecture will showcase some of VueJS, Typscript and Nuxt's core packages, module and package workflow (and Antfu's workflow).

Antfu says, 'The actual build process is part of the process, so lets see how we go.' Remember contributions and recommendations are welcome.

## [0:06:20 Project Setup](https://www.youtube.com/watch?v=49WXr6kVBVI&t=380s)

- Often Antfu defaults to his ready made templates (Vitesse or Vitesse Nuxt), in this instance will build from scratch.
- Discussion: about Antfu's settings, for this has a link with all the info [`antfu/use`](https://github.com/antfu/use).
  - `"windows.nativeTabs": true`, ... in VSCode to get the project to a tab view (MacOS only).
  - [ ni ] in the terminal, is an alias to [ npm i ] or similar, however it will automatically choose the right package manager you are using in the project. See here for more details [`antfu/ni`](https://github.com/antfu/ni).

### Installing packages & setup

- Antfu follow documentation sites and implements from scratch for this project.
  - [Nuxt docs](https://nuxt.com/docs/getting-started/installation#new-project) - choosing `npx nuxi-latest init learn.nuxt.com` .
  - [Adding Modules](https://nuxt.com/blog/v3-8#%EF%B8%8F-nitro-v27) - chosing `nuxi module add <module-name>`.
    - Adding, @vueuse/nuxt
    - Adding, @unocss/nuxt
    - Adding, @nuxt/content
    - Adding, @nuxtjs/color-mode
  - Adding Linting, see below for more details.
    Along the way, Antfu shows how tests the success of the installs.

### [UnoCSS](https://www.youtube.com/live/49WXr6kVBVI?si=DRTuSN2L_Ps10DU3&t=1022)

[UnoCSS Docs Here](https://unocss.dev/presets/uno)

- Begins with a uno.config.ts file under root directory. (Typescript should inteli-sense the options in your project.)
- A TailwindCSS alternative with more customisation.
  - Presets: [] - examples provied:
    - `presetUno`, the defaults (however does not restyle html elements, look to reset below)
    - `presetIcons`, allows to use icons as attributes
    - `presetAttributify`, allows direct writing of classes as attributes, with super powers. [* see below]
  - Within App.vue, add the `import '@unocss/reset/tailwind'` to reset the html elements. (Allows your library to have greater consistency across a variety of browsers.)

### [Nuxt Color-mode](https://www.youtube.com/live/49WXr6kVBVI?si=dFctbP0EdW3_T415&t=1171)

[Nuxt Color-mode Docs Here](https://color-mode.nuxtjs.org/)

- Discussion: difference between nuxtjs/color-mode and vueUse, color-mode... the first is SSR compatible (as persists state via cookie that can be passed to server), helps with smarts behind hydration sent down the line.
- Begin in script setup initialize a variable to useColorMode().
  - Actually, first also needs, nuxt.config.ts to have additon of `colorMode: { classSuffix: '' }`.

Footnote:

### [ESLint Formatting](https://www.youtube.com/live/49WXr6kVBVI?si=nvIzUI1oTPAeaJt3&t=1579)

- `npx @antfu/eslint-config@latest` - to install Antfu's eslint config.
- Then add script 1, `"lint": "eslint ."` to package.json.
- Then add script 2, `"format": "eslint . --fix"` to package.json.
  - Remember to ni (install) and restart editor.
  - Tip: CMD-P, Restart Extension Host, this restarts the setup of extensions within vscode to activate.

## [0:31:35 Basic Layouting](https://www.youtube.com/watch?v=49WXr6kVBVI&t=1895s)

- Note: good practice to use 2 words for component names, to avoid collision with standard html elements. TheNav is a good example to avoid collision with <nav></nav>.

### [UnoCSS - simplifying first steps](https://www.youtube.com/live/49WXr6kVBVI?si=jOIzkOTPfJqjLYtM&t=2027)

- Antfu, shows practical application of layouts.
  - Layout of SPA, will take full screen, with the panels within scrollable, so set layout for full screen.
  - `p4` is convention for 1rem.
  - `grid-cols-[1fr_2fr]` is convention for 1fr 2fr (fractional application of space) in UnoCSS leading to 2 cols.
  - Antfu, likes to apply opacity configs to e.g. `border-gray:50`.
- Antfu's personal preference is to pre-define tokens, or shortcuts for use in a design system. These are aliases. Therefore, consider the name: `border-base`, as a token instead pointed to the configuration `border-gray:50`.
  - The location UnoCSS puts these is `shortcuts: { 'border-base': 'border-gray-50' }` .
  - Note, however, we can give this border-base even more power as a token.
    - Now, with this paradigm it is also possible to extra token specificity: `border-gray-50 dark:border-red` , creating a responsive color for color-mode.
    - Benefits is that this is applied across the app consistently (and keeps code a little DRYer).

### [Logos & SVGs - simplifying first steps](https://www.youtube.com/live/49WXr6kVBVI?si=G9sIj16mJaYG8FU_&t=2710)

[icones.js.org](https://icones.js.org/)

- Demonstrates his method of using icons.
- With `presetIcons()`, can add icons as attributes.
  - Note, first step is to install the collection referenced.
    - Antfu demonstrates how to install a single iconset from [icones.js.org](https://icones.js.org/).
    - Then shows how to install all the icon sets `ni -D @iconify/json` .
    - 'You can used as a button or anything', meaning depending on the element wrapping the attribute, the svg can be used in any context you want.
- Inline classes... Antfu added additional functionality such that can drop the `class=""` syntax and simply inline the attributes.
  - Thus introducing also the 'grouping' of attributes, see presetAttributify notes above, [video example here](https://www.youtube.com/live/49WXr6kVBVI?si=RbIVecKtN9qeJRbx&t=3084).
- Antfu pulls all together with example of styling the github icon, with a hover effect.
- `<NuxtLink>`, swapped out as a more proformant option to <a></a> tag.
  - Soft routing enabled (Vue router loading vs. full page refresh).

Commit: [[/ feat: basic layout /]](https://github.com/nuxt/learn.nuxt.com/commit/95753c559964dea1f9f99a0ac0f118876918873b)

## [0:58:14 Setup WebContainers](https://www.youtube.com/watch?v=49WXr6kVBVI&t=3494s)

Reference Sites: [WebContainers.io](https://webcontainers.io/), [XTerm.JS](https://xtermjs.org/), [.getReader()](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/getReader)

- Antfu, follows documentation to implement a webcontainer.
- Documentation states warning, 'call only once'... Antfu, considers and sets up: [ /composables/webContainer.ts ]
  - Sets up guard to run only once (NH).
  - Another way of saying what are coding: 'a singleton' .
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
  - Observes, now visible. Antfu, is wondering if the later part of stream [ stream.value = devProcess.output ] is appended.
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
  - Review first contribution: about async and \_webContainer instance. Very good feedback and quick, thank you!

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
- Consider container & situation of starting server sessions within server sessions. (Instead stop the un-intended spawning of these, to allow one instance of HLR).

## [0:06:50 UI Tweaks](https://www.youtube.com/live/mDjI1uR-s-M?si=gBGANUDenMikl8gC&t=405)

### [Discussion on how to implement a desing system](https://www.youtube.com/live/mDjI1uR-s-M?si=eF6M00ycU-F1wfqY&t=1279)

Reference the new Nuxt design scheme, see [here](https://nuxt.com/blog/new-website).

- Start by loading background preset shortcuts found in uno.config.ts, 'bg-base' in this instance input hash, 'bg-[#020420]'
- Discusses pros and cons of applying a bg to the layout. Antfu's pref is to apply within app.vue, under the html or body tag. In this way, is applied across all elements.
  - If chose to use @apply (from TailwindCss) to append then shows how this is supported: need to enable this functionality in UnoCSS through 'transformers', by adding `transformerDirectives()`, which essentially a means to call in, 'special syntax inside HTML'.
  - However, syntax highlighting of vscode disagrees with this direction, so Antfu shows another built-in way from UnoCSS, `--uno: bg-base` which keeps css prompting of editor in line with expectations.
  - [*Footnote*: another exit door for @apply, is --at-apply, which also streamlines editor experience if you prefer.]
- Lets consider font use:

  - Usual way is to download specified weights and scripts, however UnoCSS has a helper here too.
  - Under presets, import then add `presetWebFonts({})`, which accepts an object to allow setup options.
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
- Nuxt Design upgrade, also implemented a [`Github Source Code`](<(https://nuxt.com/blog/new-website)>) button, that allows you to quickly deepdive into the code being discussed in the documentation.

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
- Also, has ability to introduce 'relative sizes' of e.g. p relative to h1!

Commit: [/ feat: integrate '@nuxt/content' /](https://github.com/nuxt/learn.nuxt.com/commit/b3b54c67f270a9e31be04bc5d53babd812ac0b2c)

## [0:43:42 Struggling with WebContainers](https://www.youtube.com/live/mDjI1uR-s-M?si=tdZBoCbLjp3aAhjG&t=2623)

- Next, lets make the playground represent files from focused project in the playground:
  - Within `/templates/basic/app.vue` - provide for a hello world, to update (instead of the slot) - works.
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

Commit: [/ feat: support mounted nested folder to WC /](https://github.com/nuxt/learn.nuxt.com/commit/52d87006c2d98d854b9a6edbec84d6e4c1dea59c)

- Back to original problem, Nuxt representing in WebContainer...
  - Errors present, test by regressing Nitro to an earlier version, in case due to latest.
  - Realize, with "overides" to specify the "nitropack" version, use "*~*2.7" not "*^*2.7" to prevent auto update.
  - Next... explore a Stackblitz example booting a Nuxt preview instance.
  - Consider... HTTPS, for load setting for Nitro... implement.

// PARK ... will ask around and return later.

Footnote, interesting asides:

- In terminal, can access `window.useNuxtApp()` in the session

## [1:41:00 Resizable Panels](https://www.youtube.com/live/mDjI1uR-s-M?si=RUwKWggLfJiztGfv&t=6062)

- Next, lets implement resizable windows.
- An old library that is still used for this is ['Splitpanes'](https://github.com/antoniandre/splitpanes)
  - Follows documentation for importing.
  - Styles added after the uno.css import, however not showing up... ...
    - Decide to add a dedicated `styles/overides.css` file to target and style the divider.
    - Notice, when dragging it, the grip of the mouse can lose the edge. To work around this, use point-event null.
      - The library contemplates this and has events of 'resize and resized' to allocate to 'start and end' respectively.
      - Then... conditionally add to the Playground (the listening component) not to listen to cursor event when isDragging.
  - Lets preserver the size of the window after resizing to prevent 'refresh' resetting the window.
    - Shows how to create your own limited type for a variable after investigating the output from the library.
    - Apply the width % to leftSize variable created.
    - Shows best practice to 'persist this value' with `useLocalStorage()` function from Nuxt, with a key and deafault.
    - Consider if need animation to assist UX, decide not, so remove it from the styled feature.
  - Next... apply similar styling to the horizontal dividers.
  - NOTE: we could repeat the 'isDragging' for his component as well, however Antfu instead shows how to extract it as a composable, within a state.ts file.
    - Rather than exporting a ref, shows how to export a function (which is now a composable).
    - This is an interesting pattern, when [applying the composable](https://www.youtube.com/live/mDjI1uR-s-M?si=bTZsAVfa9WRZtcAX&t=7427), through the refactor.

Commit: [/ feat: support resizable panels /](https://github.com/nuxt/learn.nuxt.com/commit/1e02d350ed972fdcda24d436d513239fcc4ba6bf)

## [2:10:00 Chat & Tools Sharing](https://www.youtube.com/live/mDjI1uR-s-M?si=44casB-Nwwk6fqam&t=7802)

- Close Playground coding session and open up for general chat about process, streaming and the tooling used.

General chat:
Mostly talking about the tooling described in [Github, Antfu Use Page](https://github.com/antfu/use).

- Re. Presets for UnoCSS, yes could autoimport the lot, however like also to allow people to consider and choose what they are using for each project.
- Discussed preferences of various settings in VSCode.
- Generally speaking, Antfu uses CMD pallette for the general dictionary of shortcuts vs setting specific keyboard shortcuts.
- Antfu uses eslint for linting and formatting and describes why [here](https://antfu.me/posts/why-not-prettier). Essentially, allows line by line control over how things are handled (with highlevel options).

### From the audience:

- To flip between start and end of open brackets: _CMD + Shift + \\_
- To jump to that line number: _CMD + P, then : with line number_

Deeper dive topics:

### Eslint settings for wrapping of lists:

- Eslint, customized his own prettier formatting preference re. first items:
  - Can change the arrangement 'all on one line' vs 'vertical list' of items, by setting preference on the first item.
  - Look for rule drafting in ['consistent-list-newline'](https://github.com/antfu/eslint-plugin-antfu/blob/main/src/rules/consistent-list-newline.md)

### Searching existing alternate code bases, while in flow:

- One good efficiency hack Antfu uses with the Tab functionality available in MacOS & VSCode is _CNT + R_ (for recent) to look (or search through) previously opened projects.
- Tip: consider _CNT + R && CMD + Enter_ on selected project, opens in a new tab.
  - Great for setting up workspaces (learning from other projects) or
  - For opening a reference project to review before writing your own.
- _CMD + P_, allows you to search for files within the project.

### [.zshrc](https://github.com/antfu/dotfiles/blob/main/.zshrc)

- Highlights a long list of aliases, within zsh, for node use.
- Simplified the 'standard call' by also simplifying the call to [ni](https://github.com/antfu/ni), which auto-selects the right package manager.
- (Notice, all aliases are simply one letter or so).

### More on Antfu's workflow

- Hub (hub.github.com) vs cli.github.com discussion.
- Clonei ... use i (for my code master folder) or f (for forked code master)
  - clonei thus, puts the code in the right place from whereever I am (and open it)
  - clonef, puts into the fork folder and opens it.
  - cloner - puts into reproduction folder and opens it.
  - codei vite - is a helper along the same lines, 'knowing you have a project, opens it quickly from whereever, in this case vite'.

### Reviewing code hacks...(NH)

Piecing together of the above... having loaded the target projects in the various folders, Antfu:

- pr function, with the number (for the pull request ticket)... when inside the repo, opens the PR in the code editor.
- then 'main' to get back out.

# Episode 3 - Pinia & Editor & Refactors

## [0:00:00 Prepare]()

## [0:08:15 Explain issue from the last episode](https://www.youtube.com/live/B7JJP-vgImM?si=tQle-dxTdfvKLK_q&t=499)

About previous episode bug / stopper:

- Antfu began investigating but guzumped by 2 of the community members following along (both submitting PRs at same time).
- Nub of issue is that Nitro initiates a number of servers and the WebContainer listen's to the last one.
- Discussed nominating a port (env), or selecting the smallest number. For now going with hard-coded 3000 port.

This code is found in merging of Issue 12 and 13, [here](https://github.com/nuxt/learn.nuxt.com/pull/13).

## [0:16:07 Merged PRs catch up](https://www.youtube.com/live/B7JJP-vgImM?si=8ayPREGERa-gFCVy&t=986)

Discuss other merged PRs, first up discussing community contributions:

- Local Cookie: switched, from `useLocalStorage('nuxt-playground-panel-left')` to a `usePanelCookie (composable...)` details [here](https://github.com/nuxt/learn.nuxt.com/pull/14).
- Npmrc: import.meta.glob, doesn't include .\* files explicitly, [so consider adding](https://github.com/nuxt/learn.nuxt.com/pull/11)? (Antfu will revisit later).
- Switch Color Styling: considered [dynamic styling](https://github.com/nuxt/learn.nuxt.com/pull/17) for change of color-mode. Antfu decides doesn't fit current use case, but good demonstration of code so calling it out, in case useful for others.
- Panel sizing: avoiding a bug if one panel is resized to 0, [here](https://github.com/nuxt/learn.nuxt.com/pull/18).

Next, discussing those UI changes Antfu made in between sessions:

- Updated, such that there is a single svg for logo.
- Improved dividers, to be more subtle.
- Added headers to each section.

Explored community ideas on design discussed:

- Adding in preset unocss for Playground. Antfu wishes to keep lean, and not add in too many dependencies, while keeping un-opinionated for projects that are loaded.
- Concept, a Search & Refresh bar: Antfu checkedout PR and discussed merits of design and direction, demonstrating how he merges such a PR: - A consideration is there is a difference between 'hard navigation' and 'soft navigation', where 'soft navigation' is referring to the navigation enabled by VueRouter (and doesn't reload the whole page). - Implements with a simplified design.
  See [here](https://github.com/nuxt/learn.nuxt.com/pull/21) for that PR merger.

## [0:35:41 Refactor components](https://www.youtube.com/live/B7JJP-vgImM?si=uVrJ2H991P-_8Q5c&t=2142)

Lets revisit the .client component:

- Antfu notes because the preview pane is rendering client only, there is a noticeable delay in the rendering of the page.
- Considering a different approaches, with a `<PanelPreview>` component:
  i. Pulling the 'initialization' of the panes on RHS to be later, while the painting of the blocks are prepared earlier.
  ii. Pulling logic from the component, to allow more easily understanding what is going on.
- Interesting turn, is that `<PanelPreview>` shares state object (:stream="stream") from the preview into the terminal pane... so consider options for that:
  - One way is again, falling back to `useState()` composable as part of a new function for the purpose of sharing (such as e.g. useTermianStream), however this feels a temporary fix, so in instead [_reaching for Pinia_](https://www.youtube.com/live/B7JJP-vgImM?si=0HDyemEOq9bnxLUt&t=2591).
  - Putting finer control to size of panes, noting horizontal spacing and vertical spacing are independent, create two different values to track.
  - Thus Antfu, shows how .client render the components still relevant, however the server now provides the content to hydrate within these components.
    - Showing how the hydration is having difficulty finding the parent element.
    - Try various ways of linking to element and resolve by using `nextTick()`.
    - Perhaps a better way is for a `watch()` component that stops after the element has appear.

Next, lets also want the server boot logic to be in its own composable... lets pause and consider all our todos currently.

## [0:56:09 Listing TODOs](https://www.youtube.com/live/B7JJP-vgImM?si=-wjb0OHtqMh_oZLk&t=3372)

- Antfu lists 6 todo items, from adding Pinia, to syncing styles.
- Then considers order of todos, as the order can help with the following component creation.
- Monaco Module - discussed as option for including. Antfu, decides to roll his own as keen to manage the integrations directly.
  - This lead to exploration of the SFC Vue Playgound, which has type support and a Monaco editor implementation.
  - However, lets avoid implementing another runtime instance of Vue when we have the Nuxt infrastructure already.
- Where does this leave us? ... Well, instead of implementing Monaco (which could take weeks), lets focus on getting an editor in its simplest form working.

## [1:06:15 Virtual File Structure](https://www.youtube.com/live/B7JJP-vgImM?si=ciEFzvFG0dUn3i6f&t=3979)

OK... so lets do the refactor of the composable and hook up basic editing in the webcontainer:

- Focus, on `startDevServer()`, placing within playground.ts.
- Consider if functions are flat, async or mounted within `<PanelPreview.client.vue>`.
  Commit: [/ refactor: moving and dividing some parts /](https://github.com/nuxt/learn.nuxt.com/commit/7daf1fed3c788a6dc174127f1b732be5b0354a3b?diff=unified&w=0)

[Next](https://www.youtube.com/live/B7JJP-vgImM?si=C7C8LSEmkIdrlt5t&t=4686)... lets consider the file we are writing to, it might be any of a number, so lets consider a virtual file system:

- First up, imagining a class File, with all the components.
  - Detailed outline of the type and file structure of the files now considered.
  - Key: made as a function `loadFiles()`, so that can load multiple times without mutating it.
  - Or... could also make reactive... with a getter() in the File...?

[_Footnote_](https://www.youtube.com/live/B7JJP-vgImM?si=0lDMB38kjCz4qE2J&t=5292): types were not 'reading in vscode descriptions' through the project, so updated nuxt.config.js to enable it so that it could.

## [1:44:00 Explain Vue reactivity unwraps](https://www.youtube.com/live/B7JJP-vgImM?si=6aY3gTjk3u97bFL6&t=3980)

- Real world example of ref v. Reference v. shallowRef, with explanation \*

* Note: to access a ref, which is nested, this value isn't unwrapped automatically, so need to use .value to access it.
* Considered using `reactive()` instead, which then discards use of .value as is automatically unwrapped.

* Noting that, however using useState with nested values we ran into roadblocks. Antfu explains with the Vue SFC playground the issues at play as a 101 on the background on Vue's reactivity system.
* Solution: can `markRaw({})` the object in order to avoid useState getting too handson with trying to assist us with a solution.

## [1:58:40 Basic Editor and HMR](https://www.youtube.com/live/B7JJP-vgImM?si=ctrpHptzFY_2rHoq&t=7123)

Consider props and `defineProps`, to pass in the file to be used in the editor.

- In this instance to pass in the files selected, why not instead start with defaults? Antfu shows, `props = withDefaults` pattern.
- Demonstrates simple presentation of files with a preview pane.
- Footnote: `of-auto` is a shortcut for overflow-auto in the viewport.
- Next, shows how can `throttledWatch` the files for changes - from VueUse.
- Demonstrates, 'text-primary' highlighting of current file, with the simple presets of UnoCSS set up in earlier classes.

Commit: [/ feat: introduce File structure and add basic editor /](https://github.com/nuxt/learn.nuxt.com/commit/0d1bc13e4aef14a0967763c1d6671e17caa09298)

## [2:15:00 Explain Vue defineProps](https://www.youtube.com/live/B7JJP-vgImM?si=VlZyM6Q6WdSkfD8e&t=8108)

Antfu runs through the syntax of various ways of declaring Props.

## [2:25:00 Refactor to Pinia](https://www.youtube.com/live/B7JJP-vgImM?si=kMmfgBgh07iL_rX4&t=8702)

Antfu gets on a march and explains the excitement of working through a clear list of todos for a new project. (Getting the mix just right between not too easy, not too hard).

- Setting up Pinia, noting... Antfu, has never used it before, so learning along with us.
- A good opportunity to show the Nuxt Devtool setup. Devtools allows a GUI for finding module and installing. The install process also forecasts what changes will be made.
  - However, cross origin policies blocked the install, so reverted to '\*' accepting all origins.
  - Devtools, works now but ....

Bug: identify cross-origin headers need to be specifically specified for the webcontainer, however this appears to be at odds with allowing devtools to work. (Will park and come back to this).

###_Pinia_
[Pinia Docs Here](https://pinia.vuejs.org/)

- Antfu, starts by playing around to experiment on how the store is initiated if called in components on the web or client.
- Considers moving the `usePlayground` into the store and then typing the environments.
- My utilising the `mount()` function on the client side, that also provides some simplification between concerns re. server vs client.

Antfu's thinking, 'Pinia, helps share state while being SSR friendly'.

Next let's consider the individual ui elements, some make sense to simply implement in state (such as `isPanelDragging`), whereas the individual values of the panel sizes would be better passed together.

- Looked at creating own {}, including Json.stringify to create own inputs, however
- Discovered Nuxt's composable `useCookie` automatically serializes and deserialize, docs revealed [here](https://nuxt.com/docs/api/composables/use-cookie).
- Antfu showed the 'traditional way' pre-Nuxt, then simplifies the code to rely on Nuxt's built in composables, which simplifies the approach a lot.

Commit: [/ feat: refactor using pinia /](https://github.com/nuxt/learn.nuxt.com/commit/9913b51d47dedfe6c0681568e309aa02b24020a4)

Observation: the `mount()` is in the store, however we only want to call and operate this once... ... so lets move it to the webcontainer. Antfu - shows refactor on this.

Qu: why useCookie over useLocalStorage? Ans: because we want the opportunity of the state to come from the server.

# [Episode 4 - Frame Communications](https://www.youtube.com/live/bUumUU8z1Oo?si=mKZ7xfwsxobKjGuY)

## [0:00:00 Preparation](https://www.youtube.com/live/bUumUU8z1Oo?si=mKZ7xfwsxobKjGuY)

- Antfu, is getting used to speaking while also coding. A new experience for him.
  Opening Code: [/ feat: show panel loading status /](https://github.com/nuxt/learn.nuxt.com/commit/f6d4f5a675774083610ee5db113f7df03a02eb17)

## [0:05:55 Changes recap](https://www.youtube.com/live/bUumUU8z1Oo?si=pRn-LwIkOH9NoqWG&t=356)

- Antfu opens editor on teh 'feat: show loading status' commit, which is 16 commits ahead the 'feat: refactor using pinia' commit of previous episode.
  Review:
- In 3rd episode of last week, we fixed `wc.on('server-ready')` composable.
- Improved text area input to code editor, for functionality.
- Other:
  - Renamed: File to VirtualFile (to avoid conflict)
  - Rename: PanelGuide to PanelDocs (to be more consistent with intent)
  - Enable minify: for production.
  - Discussed `templates/basic/basic.ts`, used for loading files: implementing an async chunk to imports, to improve performance.
  - Implemented styling for terminal.
  - Move communicaiton logic (of playground preview) to a Plugin: to consistently inject in spun up projects. (NH)
  - Frame-to-parent Communication: with WebRPC, considering as a direction for further communicaiton ability, Antfu acknowledges assistance.
  - UI Improvement: Color-mode, to pick up user's preference from the session ([commit here](https://github.com/nuxt/learn.nuxt.com/commit/d1aec8c1abaf971d4ac11074df61c86d309bc333))
  - SplitPanel: Allows work around for split-panels to work on server as well as client.
  - Progress updates: providing a progress update UI to show you the stages of the booting of progress.

## [0:21:45 Sync color mode](https://www.youtube.com/live/bUumUU8z1Oo?si=pRn-LwIkOH9NoqWG&t=1305)

Next steps: consider the preview pane, to have styles (a) in line with the surrounding styles of playground and then (b) also allow over-riding with the project app's own styles if present.

- Lets focus on the playground representation itself.
  - Demonstrates how adds `base.css` to the internal project via the `nuxt.config.ts`.
  - Next, adds an `eventListener` through the plugin architecture to listen to the parent - now listens.
  - Lets setup up a level and talk to through the iframe to let it know our color-mode.
    - Consider timing of load and presence of frame.
    - Antfu, demonstrates how to load once, then to extract as a `syncColorMode()`, which is implimented through a `watch(colorMode, syncColorMode)` watcher.
      - Discuss attribute of `{ flush: 'sync' }` within the watcher, [here](https://www.youtube.com/live/bUumUU8z1Oo?si=syd0t6PEzxWob0-A&t=2220).
      - Discuss Vite's need for pre-loading Pinia's states through HMR. Pinia allows for this functionality, see [here](https://pinia.vuejs.org/cookbook/hot-module-replacement.html) for documentation reference which Antfu implemented.
    - Antfu, now is looking at the flash and considering the inner playground instance would be better off starting in dark mode.
      - Considered (a) adding through `nuxt.config.ts` a script, but...
      - Opted for directly `htmlAttrs: { class: 'dark'}`.
      - Here is another (better) way: consider .nuxtrc file to do the same job. Script becomes: `app.head.htmAttrs.class=dark`.
    - Antfu... realises, now that we can inject the file, lets only inject if the colormode is in the beginning dark, otherwise leave as light. (And shows us how to add a file to `tree`).

## [0:55:05 Hide Nuxt Loading Screen](https://www.youtube.com/live/bUumUU8z1Oo?si=pRn-LwIkOH9NoqWG&t=3305)

Next... lets tackle the loading screen to prevent the 'Nuxt Preview' large screen:

- Nuxt Client polls the server until it is ready. Consider the loading screen template code, found [here](https://github.com/nuxt/assets/blob/main/packages/templates/templates/loading/index.html).
- Antfu shows a pattern that can hang a function call until a promise is resolved in another function.
  - Current path (implemented in the webcontainer) hitting no-cor errors, so... consider instead to implement in the iframe. (This includes a switch case for `play.status = 'ready'` within the webContainer composable.)

Commit: [/ feat: hide Nuxt loading screen /](https://github.com/nuxt/learn.nuxt.com/commit/d32311acd11564bec78357efe1dd9fc52434e83d?diff=unified&w=0)

## [1:20:30 Use RPC for communication](https://www.youtube.com/live/bUumUU8z1Oo?si=pRn-LwIkOH9NoqWG&t=4830)

RPC System: a remote proceedural call, instead of the window.addEventListeners etc. [RPC wiki, here](https://en.wikipedia.org/wiki/Remote_procedure_call).

- Antfu calls out tRPC, which is RPC with type system. This streamlines business logic communication between front end and backend.
- One good package is [tRPC.io](https://trpc.io/).
- There is also a more lightweight version (which Antfu made)... called [birpc](https://github.com/antfu/birpc). (NH: it has 0 dependencies and is circa 0.5kb).
  - BIRPC - stands for bi-directional RPC.
  - We'll go in this direction, because our instance is particular: we control both the client side and server side code; there is a low chance of missalignment of versions (in the one code base).
  - It essentially adds types to the messages.

For the coding:

- Begin with adding the types.
- Extracts the logic of the CLIENT for the messages & color change to Client & Server (renamed as FrameFunctions & ParentFunctions respectively, in this instance).
- When considering the SERVER (webContainer.ts), these functions are received in reverse. (BiRPC is isomorphic - same for both instance, but for the swapping of posts).
  - Note: there is an instance where RPC could be created, however the servers may not be there yet.k
  - Bug fix: colorMode through the implementation.

Commit: [/ add birpc for communication /](https://github.com/nuxt/learn.nuxt.com/commit/3818f938ba1d6705f397f218c7577102959acc15?diff=split&w=0)

Note:

1. If wish to add co-author for the github push, sometimes the functionality of Github / GitLens doesn't allow authors who are not already registered contributors. That said, Antfu shows a way around that, for which Github will then pick up the thread and credit them.
2. By using `close #39` or such, that links also to the issue within the Github Repo, '#' is the operator that makes that work. (Note, this automatically closes the commit as well. It also links the commit's code to the closed item.)

For a full list of the attributes that you can use, see [Github's docs here](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword).

## [2:05:00 Q&A](https://www.youtube.com/live/bUumUU8z1Oo?si=pRn-LwIkOH9NoqWG&t=7500)

- Discusses Vite's implementation of birpc.
- What tools for versioning?: bumpp...
  - Creates a tag, a new number and gitcommit
  - These are done by actions and also creates the changelog.
- Icons in browser: File Icons for Github & Gitlab (for Chrome and VSCode) - found [here](https://chromewebstore.google.com/detail/file-icons-for-github-and/ficfmibkjjnpogdcfhfokmihanoldbfe?utm_source=ext_app_menu).

# [Episode 5 - Terminal Panel & Download Zip](https://www.youtube.com/live/IJ27LUb6BAo?si=YssS3sslLE1cUddR)

## [0:00:00 Preparation]()

- Reflection: great to have Nuxt combined with Webcontainers, offering full fledged app in the container. This is a new approach, without the usual mocking that previously was use. Clean and powerful.
- Review of commits between episodes:
  - Adding type to Splitpanes, [here](https://github.com/nuxt/learn.nuxt.com/commit/6e96720af4b15aefd7ab0944d55138a89f0c0c75).
  - Enable CI for linting and types, [here](https://github.com/nuxt/learn.nuxt.com/commit/e4870bcf65882d5b03cdb8871d1569bf5def9471). Concept is later when tests are added, will also run those prior to commits.

## [0:05:00 Terminal panel toggle](https://www.youtube.com/live/IJ27LUb6BAo?si=Ds-HBUfllLy8A4Co&t=300)

Background:

- First up, discuss hiding the infrastructure of the tools.
- Probably go about this by extracting into a 'package' or 'layer'. Antfu explains how it can extend multiple apps. (Changing default Nuxt to align with scenario we want).

First up hiding the terminal:

- Discuss pros & cons of v-if, which will halt the server.
- Demonstrates v:bind process of binding classes expressed as an object, [here](https://www.youtube.com/live/IJ27LUb6BAo?si=_udpPPd9_ti6w9wx&t=1209).

Commit: [/ feat: toggle terminal /](https://github.com/nuxt/learn.nuxt.com/commit/ee11cd0ed24a98e6978ef11ac5e0bbda5fec7936)

## [0:31:50 Restart server button](https://www.youtube.com/live/IJ27LUb6BAo?si=HI5pAubJ_yJ61d6j&t=1914)

Next a server restart button:

- Consider whether want files reloaded or container restarted.
- Antfu adds types as well as `play.actions.restartServer()`... for the new function to be called on.

Commit: [/ feat: button to restart server /](https://github.com/nuxt/learn.nuxt.com/commit/2e9c245b8d5e04a5fd7682cfbf4adccb8f26f376)

## [0:46:15 Refactor playground utils into layer](https://www.youtube.com/live/IJ27LUb6BAo?si=J3VNx_0ZTiRPUsRa&t=2779)

Lets talk [Layers](https://nuxt.com/docs/getting-started/layers).

- Antfu puts subject items in a new folder, `.layer-playground`, enabling typscript support.
- Also, considers `/styles/base.css` for re-hooking that up.
- Editor now shows `.layer-playground` files. Actually can sort to exclude them, with Regex, however instead think to approach by focusing on the 'globs' of the file path... for that, looking to `ni -D micromatch`. See [fast-glob library](https://github.com/mrmlnc/fast-glob) and particularly the matching algorithm micromatch.
  - Try instead [picomatch](https://github.com/micromatch/picomatch)... as perhaps more 'inline'matching.
  - Actually, appears to be more of a node.js type implmentation, so lets do it by Regex.
- Antfu, writes Regex version.
- Consider `.nuxtrc` for mirroring (and hiding) the nuxt extends functionality implemented.
  - Antfu, [shows](https://www.youtube.com/live/IJ27LUb6BAo?si=gM6KuArP7eYJMBmE&t=4130) how can append new .nuxtrc to the existing one.
  - Shows how this streamlines the colour injection on initial load in the `webContainer.js` .

Commit: [/ feat: extract playground utils to a layer /](https://github.com/nuxt/learn.nuxt.com/commit/5119dfbe9bb8fac2b4ae7449ec64be1dbd305686)

## [1:15:30 Download the project as zip](https://www.youtube.com/live/IJ27LUb6BAo?si=H26vP2P3q5suP1Sd&t=4535)

[JSZip docs here](https://stuk.github.io/jszip/).

- Antfu demonstrates how he hunts around documentation or types to find functionality.
- Begins by setting up the types, for downloadZip, to be associated with the store and actions.
- Constucts the `downloadZip()` function
- Discuss - ghosted element (never mounted).

Commit: [/ feat: add download as zip button /](https://github.com/nuxt/learn.nuxt.com/commit/ed369cf15faa2dba4a2357d8f5312c3ff6675a99)

## [1:48:45 Random chat](https://www.youtube.com/live/IJ27LUb6BAo?si=P11QDwoZwdolZVCQ&t=6527)

- Discussion on general performance.
- Probably will continue, helps having a project with well defined goals.

# [Episode 6 - Mastering Pinia with Eduardo](https://www.youtube.com/live/kevpEOR1mrw?si=CjSqAR6b-bevPv4_)

# [0:00:00 Video Testing]()

Featuring special guest, master of Pinia, Eduardo.
Pinia docs [here](https://pinia.vuejs.org/).

# [0:01:22 Master Pinia with Eduardo](https://www.youtube.com/live/kevpEOR1mrw?si=Q-Ed949S8Sjkzxei&t=82)

- Antfu talks about Eduard helping out with a pull request for the playground.
- Eduardo through the commit points out type inference is easier, [commit](https://github.com/nuxt/learn.nuxt.com/commit/9913b51d47dedfe6c0681568e309aa02b24020a4).
- Talks about, 'letting the types flow', meaning often you don't have to be prosciptive with solutions. Pinia infers a lot from the codebases used.
- To do that, put the types as close to the variables as possible. ... ...
  ... technical issues, fixed after [here](https://www.youtube.com/live/kevpEOR1mrw?si=ZP-QCoFfCP5tV5wz&t=999).

Note: good VSCode demonstration of [LiveShare](https://code.visualstudio.com/learn/collaboration/live-share).

- Eduardo talks about the 'recoginition' capabilities of Pinia for other libraries. In that case advises Antfu to consider internalising the return, to keep actions proud (availabile).
- Antfu asks: 'Is there a difference between Pinia's actions, vs. actions i put in my own objects?'
  - Answers:
    - Can have better devtools interactions, and or pre-action activities.
    - Debouce, Undo-Redo, Error tracking (e.g. to Sentry in production) etc.
    - Actions can become in this way 'transactions', you can also... invent new patterns.
    - (Capabilities there... however, haven't really pushed the feature out there much... )
  - Antfu, considers it a bit like 'decorators'... Eduardo, yes... only syntax a little more clunky.
  - Discussions breaks new ground... re. type inference and possible mutating of objects (should you choose).
- Antfu asks: 'Is there any conventions for separating state and actions', Antfu considers the structure of the properties within the object / store is long and may benefit from sub-grouping.
  - Answer:
    - Consider properties almost like you do components, you can break them out... into other stores.
    - Sometimes it doesn't make sense to separate the properties, but you might choose to separate the logic.
    - It becomes composables within composables.
- Antfu leans towards a 'useClientOnlyStore' and 'serverStore' presented in a merged object... what do you think on that?
  - Ans, probably still struggle with where the bundling goes.
  - Could tackle by plugin.
  - Key consideration: 'only write the store once.'
  - Eduardo discusses, tention between 'configuration over convention'... ask yourself, are you saving much code, if not probably stick with convention.
- Eduardo takes over, showing his preferred approach:
  - Considers moving zip function across.
  - Store: has to be syncronous (not asyncronous).
  - Consider placement of playground within onMounted... possible to invoke on load or invoke by actions. (Antfu's requirements: immeditately but lets export a promise, so it is async).
  - Shows a hack, around naming issue (with `file: _file`).
  - Discuss shortcut CNT+D, and then
  - Alt(windows), Option(mac) for jumping multiple cursors around (equivalent of whole word and can use delete with it to)
- Antfu observes, Pinia is also a singleton, so also put WC items in the store.
  - In refactor, highlights (actions) need to be moved outside the store.
  - Then run / implement the dev server and demonstrate Vue's devtools, after finding Pinia.
  - Consider pros & cons of extracting sub-functions of the existing store (such as downloadPlayground) discuss case for both sides, [here](https://www.youtube.com/live/kevpEOR1mrw?si=4R9c14FK9pOfJOZS&t=3800).
  - Discussion re. folder structure and Pinia crawler. (It only crawls one level.)
  - Talking about studytime required for Pinia Course. With exercises could span a couple of weeks.

# [1:11:28 Changes catch up](https://www.youtube.com/live/kevpEOR1mrw?si=q1yEnhjR7qP9Hz2u&t=4288)

- Antfu talks about the changes that have been made in order to do a final review before committing, thinking how everything fits in the context of the whole app.
- Sets up a guard to return early if `!import.meta.client`, note the import.meta.client is a shortcut that other bundlers (like Vite). A variable that will be defined at build time.
  - Rollup will through this for the server bundle remove unused code.
  - Removes a guard that will never be triggered.
- Antfu demonstrates how to close live share.

Commit: [/ refactor: move playground logic into pinia store /](https://github.com/nuxt/learn.nuxt.com/commit/94a5efd71050915adedde6700d79352343bc9663)

Next, Antfu discussed the PRs between episodes.

- [Commit 47](https://github.com/nuxt/learn.nuxt.com/commit/e4456b8a7399eb33c678d9dc107977a7f0007801), preventing the ability to resize text-input areas, with `resize-none`. See [Tailwind docs](https://tailwindcss.com/docs/resize) or [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/resize) for more.
- [Chore](https://github.com/nuxt/learn.nuxt.com/commit/3272e98d4da91e28a2b013bd346df4165502830c) noting the terminal now starts hidden, changed presets, which will dynamically change when opened.
- [Chore](https://github.com/nuxt/learn.nuxt.com/commit/edfbfc54f540dbecc2353308c618c1de824b382d) removes WebQR code from startup, which is a flag that can be disabled. Antfu has a place to hide for developer ergonomics.
- [Chore](https://github.com/nuxt/learn.nuxt.com/commit/0f5f0fc0193925f7c1b859657375bd77031ad5e1) removes BIRPC into its own location hidden from the playground view. (Also makes the downloaded app more clean.)

- Antfu discusses some optimisation work he did with the startup times, [here](https://www.youtube.com/live/kevpEOR1mrw?si=NSEbreEtkua8vWJD&t=4853), with code [here](https://github.com/nuxt/learn.nuxt.com/commit/b2f2662f9b993a696d6252809253979956de7c89):

  - Optimised automatically with a flag.
  - `SSR:false`, so only one Vite server. Plan is to enable it back after content is delivered to the page.
  - `warmupEntry: false`, no need for warmup as 'entry is hit immediately'.

- [Chore](https://github.com/nuxt/learn.nuxt.com/commit/11f5b9a3dce9c0b4be040d8e9ab594f3de1d721f) shows how to enable ESLint for CSS (achieved with a single line).

Then discusses what todo next with the time allotted... decide to look to read and setup Monaco Editor.

# [1:25:50 Monaco Editor Setup (struggling)](https://www.youtube.com/live/kevpEOR1mrw?si=-2eEw2RgacJZGo2c&t=5150)

- Antfu understands Monaco Editor is extracted from VSCode, [Github Repo](https://github.com/microsoft/monaco-editor) and [Documention Site](https://microsoft.github.io/monaco-editor/), however found no guide.
- Instead, looks to Samples section and in picks up Vite-React project.
- Antfu demontrates transition from React to Vue though setting up the `PanelEditorClient.client.vue`.
  - Shows hack for 'ensuring always true' before running, `el.value!`.
  - Links the more specific editor as a sub-component to `PanelEditor.vue`.
  - [Links](https://www.youtube.com/live/kevpEOR1mrw?si=NWRZ3bVDNSK9fZ4c&t=5798) file selection to active view of editor. Achieves this through a `watchEffec()`.
  - Sets up `UserWorker` for the editor to apply styles (& syntax highlighting).
    - Antfu shows how to import Types for the file copied across, using Typescipts `<reference types="vite/client">`, which works.
    - Now considers file extensions, to setworker actions depending on file selected, works.
    - Next, lets consider typescript.
      - Appears need to pass a Uri.
      - Appears need to create a model.
      - Appears model needs to be cached.
    - Next, reviews new source, [Nuxt Monaco](https://github.com/e-chan1007/nuxt-monaco-editor) editor module.
  - Antfu, considers using the Monaco Editor Module instead of writing a custom one.
    - Antfu implements, and discovers same error.
    - Tries one time more with custom direction, this time considering Vite has established a conflict, so:
      - Removes the cache and
      - Backs out some of the optimisation, with respect to Monaco.

Considering time in recording this ep. and where we are at, Antfu call break here.
General discussion:

- It would be good if guides were put up on the Monaco website.
- Could show pathway for integrating with frameworks, also noting Volar should be implemented.
- Volar is becoming a universal (Vue, Sveltte, Astro) IDE plugin.

Before closing, Antfu reviews before committing only the code that is required.

[Commit: / feat: setup basic monaco editor /](https://github.com/nuxt/learn.nuxt.com/commit/c99874d9fac39382f13b33af218504959c89280f).
