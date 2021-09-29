---
title: Leak3 CDN
patch_from: "leak2-magic/patch2"
---

* Open the Memory profiler in Chrome
* Click the red button, all the `x-for` components are removed.
* Click the garbage icon in the profiler to force GC.
* Click on the round button to create a new profile.
* Filter by `Detached HTMLTemplateElement`

You should now see 20 detached elements. If you click on one, it points to `evaluatorMemo`.

{{< main.inline >}}
<script>
    document.addEventListener('alpine:init', () => {
        Alpine.store('mystore', {
           images: ['olavstedje.jpg', "claudia.jpg"],
 
           
        })
    })
</script>
 <button x-data class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded" @click="document.querySelectorAll('.removeme').forEach(e => e.remove());">Remove Components</button>
{{< /main.inline >}}

## To be removed

{{< c1.inline >}}
{{ range seq 20 }}
{{ $v := printf "color%d" . }}
<div class="removeme" x-data="{}">
  <template x-for="image in $store.mystore.images">
    <img class="p-4 border-4 bg-green-300" :src="image" @load="$event.target.classList.remove('bg-green-300')">
  </template>
</div>
{{ end }}
{{< /c1.inline >}}

