---
title: Leak1 CDN
---

* Open the Memory profiler in Chrome
* Click the red button, all the `x-for` components are removed.
* Click the garbage icon in the profiler to force GC.
* Click on the round button to create a new profile.
* Filter by `Detached HTMLTemplateElement`

You should now see 20 detached elements. If you click on one, it points to `evaluatorMemo`.

{{< main.inline >}}
 <button x-data class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded" @click="document.querySelectorAll('.removeme').forEach(e => e.remove());">Remove Components</button>
{{< /main.inline >}}

## To be removed

{{< c1.inline >}}
{{ range seq 20 }}
{{ $v := printf "color%d" . }}
<ul class="removeme" x-data="{ {{$v}}s: ['Red', 'Orange', 'Yellow'] }">
  <template x-for="{{$v}} in {{$v}}s">
    <li x-text="{{$v}}"></li>
  </template>
</ul>
{{ end }}
{{< /c1.inline >}}
