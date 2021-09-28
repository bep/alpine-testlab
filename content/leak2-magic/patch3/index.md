---
title: x-data magics patch2
---

Note that this runs with [this patch](https://github.com/bep/alpine/commit/9dfe0c4b3bd5aeebd802e55910df79ed5ad07ea6) on top of all the previous patches in that branch -- which makes the `$watch` "element bound".

* Open the Memory profiler in Chrome
* Click the red button, all the components below are removed.
* Click the garbage icon in the profiler to force GC.
* Click on the round button to create a new profile.
* Filter by  Detached HTMLDivElement`

You should now see 0 detached elements. 

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

