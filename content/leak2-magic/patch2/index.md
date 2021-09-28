---
title: x-data magics patch1
---

Note that this runs with [this patch](https://github.com/bep/alpine/commit/6c14dfc245d063382d80dfd5518bb8ad07edf017) on top of all the previous patch in that branch -- adding a cleanup step for `injectMagics`.

* Open the Memory profiler in Chrome
* Click the red button, all the components below are removed.
* Click the garbage icon in the profiler to force GC.
* Click on the round button to create a new profile.
* Filter by  Detached HTMLDivElement`

You should now see 20 detached elements. If you click on one, it points to `el > raw> > targetMap > store ...` and similar.

This means that this still leaks, but differently than in [patch1](../patch1).

This story continues in [patch3](../patch3).


{{< main.inline >}}
<script>
    document.addEventListener('alpine:init', () => {
        Alpine.store('mystore', {
            on: false,
 
            toggle() {
                this.on = ! this.on
            }
        })
    })
</script>

 <button x-data class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded" @click="document.querySelectorAll('.removeme').forEach(e => e.remove());">Remove Components</button>
{{< /main.inline >}}

## To be removed

{{< c1.inline >}}
{{ range seq 20 }}
{{ $v := printf "color%d" . }}
<div class="removeme mb-4" x-data="{ counter: 1 }" x-init="$watch('$store.mystore.on', () => counter++ )">
  <span x-text="counter"></span>
  <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-2 rounded" @click="$store.mystore.toggle()" >Click Me!</button>
</div>
{{ end }}
{{< /c1.inline >}}

