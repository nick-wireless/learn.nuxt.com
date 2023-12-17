
[## Chapter 1 - UI Tweaks](https://www.youtube.com/live/mDjI1uR-s-M?si=gBGANUDenMikl8gC&t=405)
Anthony would love to progress the project together, feel free to jump in yourself.
Reviewing commits between videos:
- FitAddon from 'xterm-addon-fit', allows the terminal component to resize dynamically
- Repositioned color-mode button to the top.

Loads up page...
- Note, styles of booted 'nuxt project' have a glitch
    - Consider that file is there but reading as HTML not css.
    - Shows how to identify css location.
    - Park issue for now and revert later.
- Consider container & situation of starting server sessions within server sessions.  (Instead stop the un-intended spawning of these, to allow one instance of HLR).

[### Discussion on how to implement a desing system](https://www.youtube.com/live/mDjI1uR-s-M?si=eF6M00ycU-F1wfqY&t=1279)
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

Commit: / feat: align with nuxt.com design /

[## Chapter 2 - Setup Nuxt Content](https://www.youtube.com/live/mDjI1uR-s-M?si=9tcwjc9XRu8xbmrH&t=2181)
- Confirms Nuxt Content was added in earlier session, next follow docs... ... [Nuxt Content Docs](https://content.nuxt.com/get-started/installation)
- Add within a new folder, Content and index.md file, which is the start of the content presented, beginning with the index file.
- Under pages/[...slug].vue add a <ContentDoc /> component was the example from the docs website, however Antfu shows how can call in a page directly with simply the <ContentDoc /> component.
- Next: consider how you might apply styles to this component...
    - Not so obvious from the Nuxt Content Docs, so instead reverted to [UnoCSS Typography](https://unocss.dev/presets/typography) and use those tools.
- Shows how pages directly dynamically establishes routes for the content in the Content folder, by renaming or introducing the page [...slug].vue.

Interesting asides (exploring the links provided):
- UnoCSS Typography has a great set of [preset colors](https://unocss.dev/presets/typography#colors) that can be applied to make your fonts look professional.
- Also, has ability to introduce 'relative sizes' of e.g. p vs h1!

Commit: / feat: integrate '@nuxt/content' /


[## Chapter 3 - Struggling with WebContainers](https://www.youtube.com/live/mDjI1uR-s-M?si=tdZBoCbLjp3aAhjG&t=2623)
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

Interesting asides:
- In terminal, can access window.useNuxtApp() in the session


[## Chapter 4 - Resizable Panels](https://www.youtube.com/live/mDjI1uR-s-M?si=RUwKWggLfJiztGfv&t=6062)
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


[## Chapter 5 - Chat & Tools Sharing](https://www.youtube.com/live/mDjI1uR-s-M?si=44casB-Nwwk6fqam&t=7802)
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


