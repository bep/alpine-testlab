---
title: x-data magics patch1
---

Note that this runs with [this patch](https://github.com/bep/alpine/commit/6c14dfc245d063382d80dfd5518bb8ad07edf017) on top of all the previous patch in that branch -- adding a cleanup step for `injectMagics`.

{{% instructions %}}

There, you will see detached elements matching the below. If you click on one, it points to `el > raw> > targetMap > store ...` and similar.

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

{{< /main.inline >}}

{{< create-leak >}}

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

