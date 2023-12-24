
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

