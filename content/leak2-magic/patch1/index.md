---
title: x-data magics leak
patch_from: "leak1/patched"
weight: 20
---

Note that this runs with a patch for #2126.

{{% instructions %}}

There, you will see detached elements matching the below. If you click on one, it points to `get $el` and similar.

This story continues in [patch2](../patch2).

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

