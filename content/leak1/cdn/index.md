---
title: Leak1 CDN
weight: 10
---

{{% instructions %}}

There, you will see 20 detached elements. If you click on one, it points to `evaluatorMemo`.

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

