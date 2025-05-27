---
title: Add Carousel to the Document
menuTitle: Carousel
weight: 40
# for carousel
carousel: 
    - image: building.jpg
      caption: Building
    - image: lab.jpg
    - image: meeting.png
      caption: Meeting
    - image: plaza.jpeg
      caption: Open Space
    - image: work.jpg
      caption: Work
---



To add carousel effects to a page, you will need to add the following markdown in the front matter yaml part at the top of 
the md file:

```yaml
---
title: ...
menuTitle: ...
weight: ...

# Add the following for carousel effects with 4 images
carousel: 
    - image: building.jpg
      caption: Building
    - image: lab.jpg
      # The caption field is optional
      # caption: Lab
    - image: meeting.png
      caption: Meeting
    - image: plaza.jpeg
      caption: Open Space
    - image: work.jpg
      caption: Work
---
```

Then you can put this code in your page:

```html

{{</* carousel */>}}

```


{{< carousel >}}
