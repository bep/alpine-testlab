---
title: Leak1 Patched
---

Note: This version has this patch applied: https://github.com/bep/alpine/commit/c3fbc6319f2b959bfc17a67ce21677fcec386d7f -- and should give 0 detached elements.

{{% instructions %}}

There, filter by `Detached HTMLTemplateElement`, you should see 20 detached elements. If you click on one, it points to `evaluatorMemo`.

{{< create-leak >}}


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

