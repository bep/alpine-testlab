---
title: Last survives, CDN
weight: 10
---

{{% instructions %}}

The components to be removed looks like this:

```html
<div class="removeme" x-data >
    This should be removed.
</div>
<ol class="removeme" x-data>
    <li>This should be removed.</li>
</ol>
<ul class="removeme" x-data>
    <li>This should be removed.</li>
</ul>
```

All but the last component is removed correctly (and yes, I have tried switching them around).

{{< create-leak >}}

## To be removed

{{< c1.inline >}}

<div class="removeme" x-data >
    This should be removed.
</div>
<ol class="removeme" x-data>
    <li>This should be removed.</li>
</ol>
<ul class="removeme" x-data>
    <li>This should be removed.</li>
</ul>
{{< /c1.inline >}}

