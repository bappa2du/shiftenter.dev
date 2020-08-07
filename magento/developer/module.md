---
description: Magento 2 module customization
---

# Module

### Allow webp image in magento

in module's **di.xml** file add as following

```text
<type name="Magento\Cms\Model\Wysiwyg\Images\Storage">
        <arguments>
            <argument name="extensions" xsi:type="array">
                <item name="allowed" xsi:type="array">
                    <item name="webp" xsi:type="string">image/webp</item>
                </item>
                <item name="image_allowed" xsi:type="array">
                    <item name="webp" xsi:type="string">image/webp</item>
                </item>
            </argument>
        </arguments>
    </type>
```

{% hint style="info" %}
For SVG image the item node will be as
{% endhint %}

```text
<item name="svg" xsi:type="string">image/svg+xml</item>
```

